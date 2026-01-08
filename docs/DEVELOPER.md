# Developer Documentation

## Overview

The ROE/EOE Assessment is a web-based organizational effectiveness survey built with vanilla HTML, CSS, and JavaScript. It connects to a Clarion-based backend API for test validation and result storage.

## File Structure

```
roe/
├── roe-assessment.html      # Spanish version (ROE - Resultados Orientados al Entorno)
├── roe-assessmenti.html     # English version (EOE - Effectiveness Oriented Survey)
├── frasROE.json             # Assessment questions data (Spanish)
├── frasROE-clean.json       # Cleaned questions data
├── CLAUDE.md                # AI assistant instructions
├── README.md                # Project overview
└── docs/
    ├── DEVELOPER.md         # This file
    ├── USER.md              # End-user documentation
    └── INSTRUCTIONS.md      # Survey instructions
```

## Architecture

### Frontend
- Single-page application (SPA) with multiple screens
- No framework dependencies - vanilla JavaScript
- Responsive design with CSS Grid/Flexbox
- Font Awesome icons via CDN

### Backend API
- Base URL: `https://apitests.reddinassessments.com`
- Endpoints:
  - `GET /wsGetinvitRoe?id={testId}` - Validate test and get configuration
  - `POST /wsSaveInvitRoe` - Submit completed assessment

## API Reference

### wsGetinvitRoe

Validates a test invitation and returns configuration.

**Request:**
```
GET /wsGetinvitRoe?id={testId}
```

**Response:**
```json
{
  "wsGetinvitROE_response": {
    "resultComplete": "1",           // "1" = valid, "2" = already completed
    "groups": "1,2,3,4,5,6,7,8",     // Comma-separated group numbers
    "roe:pedirnombre": "1",          // "1" = show field, "0" = hide
    "roe:pedirapellido": "1",
    "roe:pedirempresa": "0",
    "roe:pedirpuesto": "0",
    "roe:pedirdepartamento": "0",
    "roe:pediredad": "0",
    "roe:pediraempresa": "0",
    "roe:pedirgenero": "0",
    "roe:pedirnota1": "0",
    "roe:pedirnota2": "0",
    "roe:pedirciudad": "0",
    "roe:pedirpais": "0",
    "roe:pediremail": "1",
    "roe:pedirsmsphone": "0"
  }
}
```

### wsSaveInvitRoe

Submits completed assessment results.

**Request:**
```json
POST /wsSaveInvitRoe
Content-Type: application/json

{
  "id": "test-id-here",
  "testdata": {
    "guid": "unique-session-guid",
    "userInfo": {
      "firstName": "John",
      "lastName": "Doe",
      "email": "john@example.com",
      ...
    },
    "answers160": "1010110010...",   // 160-character string of 0s and 1s
    "totalQuestions": 80,
    "completedAt": "2024-01-15T10:30:00.000Z",
    "testId": "test-id-here"
  }
}
```

**Response:**
```json
{
  "wsSaveInvitROE_response": {
    "resultComplete": "1"    // "1" = success, "-1" = error
  }
}
```

## Data Structure

### Assessment Groups

| Group | Type | Description |
|-------|------|-------------|
| 1-8 | DCO | Organizational Culture Diagnostic |
| 9-16 | ROR | Results-Oriented Relationships |

### Question Object
```javascript
{
  "texto": "Question text here",
  "grupo": 1,        // Group number (1-16)
  "orden": 161       // Order position (1-160 for scoring)
}
```

### Answer String Format
- 160-character string of `0`s and `1`s
- Position corresponds to `orden` field (1-indexed)
- `0` = No/Disagree, `1` = Yes/Agree

## Field Mapping

| API Flag | Form Field ID | Description |
|----------|---------------|-------------|
| `roe:pedirnombre` | `firstName` | First name |
| `roe:pedirapellido` | `lastName` | Last name |
| `roe:pedirempresa` | `company` | Company |
| `roe:pedirpuesto` | `position` | Position |
| `roe:pedirdepartamento` | `department` | Department |
| `roe:pediredad` | `age` | Age |
| `roe:pediraempresa` | `yearsInCompany` | Years in company |
| `roe:pedirgenero` | `gender` | Gender |
| `roe:pedirnota1` | `note1` | Custom note 1 |
| `roe:pedirnota2` | `note2` | Custom note 2 |
| `roe:pedirciudad` | `city` | City |
| `roe:pedirpais` | `country` | Country |
| `roe:pediremail` | `email` | Email |
| `roe:pedirsmsphone` | `phone` | Phone |

## Application State

```javascript
const app = {
  testId: null,              // From URL parameter
  guid: null,                // Unique session identifier
  userInfo: {},              // Collected demographic data
  selectedGroups: [],        // Groups to assess (from API)
  questions: [],             // Randomized questions array
  answers: [],               // User responses
  currentQuestion: 0,        // Current question index
  requiredFields: [],        // Fields to display (from API)
  isResuming: false          // Resume from localStorage
};
```

## LocalStorage

Progress is automatically saved to localStorage with key `roe_test_{testId}`:

```javascript
{
  userInfo: {},
  selectedGroups: [],
  questions: [],           // Preserves randomization
  answers: [],
  currentQuestion: 0,
  guid: "...",
  lastSaved: "ISO timestamp"
}
```

## Screen Flow

1. **Test Validation Screen** - Validates test ID via API
2. **User Info Screen** - Collects demographic data (configurable fields)
3. **Question Screen** - Displays questions one at a time
4. **Summary Screen** - Review and submit

## Key Functions

| Function | Description |
|----------|-------------|
| `validateTest()` | Validates test ID and configures fields |
| `configureFormFields()` | Shows/hides demographic fields based on API |
| `prepareQuestions()` | Randomizes questions using Fisher-Yates |
| `displayQuestion()` | Renders current question |
| `handleAnswer()` | Records user response |
| `submitAssessment()` | Sends results to API |
| `saveProgress()` | Saves to localStorage |
| `loadExistingProgress()` | Restores from localStorage |

## Customization

### Adding New Fields
1. Add HTML form field with `data-field="fieldName"` attribute
2. Add mapping in `fieldMapping` object
3. Add to `allFields` array in `configureFormFields()`

### Modifying Styles
- Colors defined in CSS variables at top of `<style>` block
- Professional color scheme: Navy (#1a365d), Teal (#0d9488), Slate grays

## Debug Mode

Press the debug button (if enabled) to auto-fill the test with random answers for testing purposes.

## Error Handling

- API errors show modal dialogs
- Network failures allow local save as fallback
- Invalid test IDs redirect to error screen
- `console.error` used for actual errors only

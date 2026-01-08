# ROE/EOE Assessment

Organizational effectiveness assessment module for the Clarion 12 assessment platform.

- **ROE** (Spanish): Resultados Orientados al Entorno
- **EOE** (English): Effectiveness Oriented Survey

## Documentation

| Document | Description |
|----------|-------------|
| [Developer Guide](docs/DEVELOPER.md) | Technical documentation, API reference, architecture |
| [User Guide](docs/USER.md) | End-user documentation for survey participants |
| [Instructions](docs/INSTRUCTIONS.md) | Survey instructions and assessment dimensions |

## Files

| File | Description |
|------|-------------|
| `roe-assessment.html` | Spanish-language assessment interface |
| `roe-assessmenti.html` | English-language assessment interface |
| `frasROE.json` | Assessment questions and response templates |

## Quick Start

Access the survey via URL with test ID parameter:
```
roe-assessment.html?id=YOUR_TEST_ID      # Spanish
roe-assessmenti.html?id=YOUR_TEST_ID     # English
```

## Assessment Structure

The assessment measures 16 organizational dimensions:

### DCO (Organizational Culture Diagnostic) - Groups 1-8
1. Productivity Standards
2. Management Competence
3. Organizational Structure
4. Communication
5. Conflict Management
6. Human Resources
7. Participation
8. Innovation

### ROR (Results-Oriented Relationships) - Groups 9-16
9. Boss-Subordinate Alignment
10. Managing Direct Reports
11. Peer Collaboration
12. Authority & Responsibility
13. Resources
14. Change Readiness
15. Results Orientation Benefits
16. Information Quality

## API Integration

Connects to `apitests.reddinassessments.com`:
- `wsGetinvitRoe` - Test validation and configuration
- `wsSaveInvitRoe` - Submit assessment results

## Configuration

Demographic fields are controlled by API flags. When set to `"1"`, the field is displayed:

| API Flag | Field |
|----------|-------|
| `roe:pedirnombre` | First Name |
| `roe:pedirapellido` | Last Name |
| `roe:pedirempresa` | Company |
| `roe:pedirpuesto` | Position |
| `roe:pedirdepartamento` | Department |
| `roe:pediredad` | Age |
| `roe:pediraempresa` | Years in Company |
| `roe:pedirgenero` | Gender |
| `roe:pedirnota1` | Note 1 |
| `roe:pedirnota2` | Note 2 |
| `roe:pedirciudad` | City |
| `roe:pedirpais` | Country |
| `roe:pediremail` | Email |
| `roe:pedirsmsphone` | Phone |

## License

Proprietary - Reddin Assessments

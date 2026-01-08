# ROE Assessment

ROE (Results-Oriented Environment) assessment module for the Clarion 12 assessment platform. This assessment measures organizational effectiveness across multiple dimensions.

## Files

- `roe-assessment.html` - Spanish-language ROE assessment web interface
- `roe-assessmenti.html` - English-language ROE assessment web interface
- `frasROE.json` - Assessment questions and response templates

## Assessment Structure

The ROE assessment is organized into 16 groups measuring different organizational dimensions:

### DCO (Organizational Culture Diagnostic) Groups 1-8:
1. Productivity Standards
2. Management Competence
3. Organizational Structure
4. Communication
5. Conflict Management
6. Human Resources
7. Participation
8. Innovation

### ROR (Results-Oriented Relationships) Groups 9-16:
9. Boss-Subordinate Alignment
10. Managing Direct Reports
11. Peer Collaboration
12. Authority & Responsibility
13. Resources
14. Change Readiness
15. Results Orientation Benefits
16. Information Quality

## API Integration

The assessment interfaces connect to `apitests.reddinassessments.com` for:
- Test validation (`wsGetinvitRoe`)
- Saving responses (`wsSaveRoeAnswers`)

## Configuration

Demographic fields are controlled by API flags (e.g., `roe:pedirnombre`, `roe:pediremail`). When set to `"1"`, the corresponding field is displayed to the user.

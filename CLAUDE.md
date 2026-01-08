# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This directory contains data files for the ROE (Results-Oriented Environment) assessment module, which is part of a larger Clarion 12 assessment platform. The ROE assessment measures organizational effectiveness across multiple dimensions.

## Directory Contents

- `frasROE.json` - Spanish-language assessment questions and response templates for the ROE diagnostic tool

## Data Structure

The `frasROE.json` file contains an array of assessment items with the following structure:
- `numero`: Question number
- `idioma`: Language code (ESP for Spanish)
- `texto`: Question text
- `tipotest`: Test type (DCO or ROR)
- `grupo`: Group number (1-16)
- `orden`: Display order
- `texto2`: Response template with `++porcentaje++` placeholder

## Assessment Groups

The ROE assessment is organized into 16 groups measuring different organizational dimensions:

### DCO (Diagnóstico de Cultura Organizacional) Groups 1-8:
1. **Productivity Standards** - Focus on efficiency and performance
2. **Management Competence** - Leadership effectiveness
3. **Organizational Structure** - Hierarchy and authority clarity
4. **Communication** - Information flow and meetings
5. **Conflict Management** - Productive disagreement handling
6. **Human Resources** - Talent development and fairness
7. **Participation** - Employee involvement in decisions
8. **Innovation** - Creativity and new ideas

### ROR (Results-Oriented Relationships) Groups 9-16:
9. **Boss-Subordinate Alignment** - Goal setting with supervisors
10. **Managing Direct Reports** - Leadership of team members
11. **Peer Collaboration** - Working with colleagues
12. **Authority & Responsibility** - Role clarity
13. **Resources** - Access to necessary tools and support
14. **Change Readiness** - Adaptability and flexibility
15. **Results Orientation Benefits** - Impact of focus on outcomes
16. **Information Quality** - Accuracy and timeliness of data

## Integration with Clarion Platform

This data file is likely consumed by Clarion applications in the parent directories (apiTests, degPwa, etc.) to:
- Generate assessment questionnaires
- Process responses and calculate scores
- Create reports with the texto2 templates replacing `++porcentaje++` with actual percentages

## Common Development Tasks

Since this is a data-only directory:
- **Updating Questions**: Edit the `frasROE.json` file directly
- **Adding Languages**: Create new JSON files with appropriate language codes
- **Testing**: Changes should be tested within the consuming Clarion applications

## Notes

- All text is in Spanish; English translations may exist in other directories
- The `++porcentaje++` placeholder is replaced with calculated percentages in reports
- Question numbers are not sequential, suggesting some items may have been removed or reserved
- Test types DCO and ROR represent different assessment methodologies
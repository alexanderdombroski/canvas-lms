# Feature: Inline File Viewing for Code Submissions

## Design

This feature enables inline viewing of common code files (e.g., `.py`, `.ts`) directly within submission comments on Canvas. Instead of displaying only metadata (filename and size), the system will render the file contents in a readable format.

Key design elements:
- Detect supported file types by extension
- Fetch and safely render file contents
- Embed the rendered view within the submission details UI
- Fallback to existing behavior for unsupported file types

## Functional Requirements
- The system shall recognize supported file types (e.g., `.py`, `.ts`)
- The system shall display file contents inline within submission comments
- The system shall use even character spacing like code editors
- The system shall preserve formatting (indentation, line breaks)
- The system shall fall back to existing behavior for unsupported files

## Non-Functional Requirements
- Performance: File rendering should not significantly delay comment loading
- Security: Prevent execution of embedded code (sanitize all content)
- Scalability: Handle large files with truncation or lazy loading
- Usability: Ensure readability across devices and screen sizes
- Accessibility: Support screen readers and keyboard navigation

## Codebase Findings
- Current implementation only surfaces file metadata (name and byte size)
- File storage/retrieval APIs already exist and can be reused
- Comment rendering pipeline can be extended to include file previews
- Potential need to modify frontend components responsible for comment display

## Testing Plan
- Unit Tests:
  - File type detection logic
  - Content sanitization
  - Rendering logic for supported vs unsupported files

- Integration Tests:
  - End-to-end rendering within submission comments
  - API interaction for fetching file contents

- UI Tests:
  - Verify syntax highlighting accuracy
  - Check expand/collapse behavior
  - Validate responsiveness across devices

- Edge Cases:
  - Large files (ensure truncation or lazy loading works)
  - Unsupported or corrupted files
  - Files with special characters or unusual encodings

- Security Tests:
  - Ensure no executable scripts run in rendered output
  - Validate proper escaping of HTML/JS content

## Agent

Use the [Analyze Repo Agent](.gemini/agents/analyze-repo.agent.md) to get general repository information

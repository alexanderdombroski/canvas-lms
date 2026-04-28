# Feature: Inline File Viewing for Code Submissions

## Design
This feature enables inline viewing of common code files (e.g., `.py`, `.ts`) directly within submission comments on Canvas. Instead of displaying only metadata (filename and size), the system will render the file contents in a readable, syntax-highlighted format.

Key design elements:
- Detect supported file types by extension
- Fetch and safely render file contents
- Apply syntax highlighting for readability
- Embed the rendered view within the submission comment UI
- Provide fallback to existing behavior for unsupported file types

## Functional Requirements
- The system shall recognize supported file types (e.g., `.py`, `.ts`)
- The system shall display file contents inline within submission comments
- The system shall preserve formatting (indentation, line breaks)
- The system shall apply syntax highlighting based on file type
- The system shall allow users to expand/collapse large files
- The system shall fall back to filename + size display for unsupported files

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
- No existing syntax-highlighting utility integrated (may require adding a library)
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
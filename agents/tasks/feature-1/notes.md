[ui/features/speed_grader/jquery/speed_grader.tsx](ui/features/speed_grader/jquery/speed_grader.tsx)

- renderAttachment()

 The functions in ui/features/speed_grader/jquery/speed_grader.tsx responsible for displaying the file are:

   1. renderAttachment(attachment: Attachment): This is the primary entry point for rendering an individual attachment. It decides
      which preview method to use:
       * DocViewer: Calls loadDocPreview if attachment.canvadoc_url is present.
       * Google Previews: Calls loadDocPreview for previewable content types if not disabled.
       * Direct Browser Rendering: Uses attachmentIframeContents for files matching browserableCssClasses (currently
         /^(image|html|code)$/).

   2. attachmentIframeContents(attachment: Attachment, domElement = 'iframe'): This function generates the HTML string used to
      populate the $iframe_holder.
       * It currently handles image files using an <img> tag.
       * For other browserable types (like html and code), it defaults to creating an <iframe> using
         SpeedgraderHelpers.buildIframe.

   3. loadSubmissionPreview(attachment: Attachment | null, submission: HistoricalSubmission | null): This function orchestrates
      which high-level preview to show (e.g., a specific attachment, a quiz, or the main submission URL). It calls
      renderAttachment when a specific file is selected from the sidebar.

  Other files that need to be edited:

   * app/models/attachment.rb: This file contains the valid_content_types_hash which maps MIME types to mime_class. To ensure
     python files are identified as code or a new text class, you may need to add text/x-python or similar mappings here.
   * packages/canvas-rce/src/common/mimeClass.js: This file contains a client-side version of the MIME mapping logic that must be
     kept in sync with the Ruby model.
   * app/views/submissions/show_preview.html.erb: If you want the python file to also render using <pre> when viewed via the main
     submission preview URL (which uses an iframe pointing to this Rails view).
   * ui/features/speed_grader/jquery/speed_grader_helpers.ts: If you need to add a helper function for fetching file content or
     building the <pre> tag structure.

  Implementation Strategy:
  To implement the <pre> display, you would likely modify renderAttachment in speed_grader.tsx to detect python files (e.g.,
  attachment.display_name.endsWith('.py')), fetch their raw content via AJAX, and then update $iframe_holder with a <pre> tag
  containing that content.
## Frames and Iframes

In HTML, frames (`<frame>` and `<iframe>` elements) allow a page to be embedded in a page. This special behaviour provides some complications in Watir.

When using a browser's developer tools to inspect elements in a frame, you will see the hosting page (`html` element`), the `iframe` and then the nested page (another `html` element):

{lang="html"}
~~~~~~~~	
<html>
  <head></head>
  <body>
    <div>content before frame</div>
    <iframe src="frame_content.htm" id="frame_content">
      #document
      <html>
        <head></head>
        <body>
          <div id="in_frame">content in frame</div>
        </body>
      </html>
    </iframe>
    <div>content after frame</div>
  </body>
</html>
~~~~~~~~

If you take the normal approach to locating elements within the frame, an exception will occur:

{lang="ruby"}
~~~~~~~~
browser.div(id: 'in_frame').text
#=> Watir::Exception::UnknownObjectException
~~~~~~~~

From the browser's perspective, it only sees the hosting page's source. In other words, the frame contents look empty:

{lang="html"}
~~~~~~~~	
<html>
  <head></head>
  <body>
    <div>content before frame</div>
    <iframe src="frame_content.htm" id="iframe_content"></iframe>
    <div>content after frame</div>
  </body>
</html>
~~~~~~~~

To locate elements within a frame, Watir must be explicitly told to do so:

{lang="ruby"}
~~~~~~~~
browser.iframe(id: 'frame_content').div(id: 'in_frame').text
#=> "content in frame"
~~~~~~~~


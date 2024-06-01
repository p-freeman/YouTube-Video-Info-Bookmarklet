# YouTube Video Info Bookmarklet

This bookmarklet extracts the title, channel name, and URL of a YouTube video and copies them to the clipboard. It is useful for quickly capturing information about a YouTube video for reference or sharing.

## How to Use

1. Create a new bookmark in your browser's bookmark bar.
2. Edit the bookmark and set the name to something descriptive like "YouTube Video Info".
3. Copy the following code:
   ```javascript
   javascript:(function() {
       function copyToClipboard(text) {
           var textarea = document.createElement('textarea');
           textarea.value = text;
           document.body.appendChild(textarea);
           textarea.select();
           try {
               var successful = document.execCommand('copy');
               var msg = successful ? 'successful' : 'unsuccessful';
               alert('Copying text command was ' + msg + ':\n\n' + text);
           } catch (err) {
               alert('Oops, unable to copy: ' + err);
           }
           document.body.removeChild(textarea);
       }

       var titleElement = document.querySelector('yt-formatted-string.style-scope.ytd-watch-metadata');
       var title = titleElement ? titleElement.innerText : 'Title not found';

       var channelElement = document.querySelector('a.yt-simple-endpoint.style-scope.yt-formatted-string');
       var channelName = channelElement ? channelElement.innerText : 'Channel not found';

       var url = window.location.href;

       var textToCopy = `${title}\n${url}\n${channelName}`;
       copyToClipboard(textToCopy);
   })();

4. Paste the code into the URL/Location field of the bookmark.
5. Save the bookmark.

## Output Format
The bookmarklet copies the following information to the clipboard:

[Video Title]  
[URL]  
[Channel Name]

Replace [Video Title], [URL], and [Channel Name] with the actual title, URL, and channel name of the YouTube video respectively.

## Note
- This bookmarklet is designed for use on standard YouTube video pages. If the layout or class names change, the bookmarklet may need to be updated.
- The bookmarklet seems to work on Firefox, where the Unhook-Addon was installed and used on a Youtube-Video (See https://unhook.app/ and https://addons.mozilla.org/en-US/firefox/addon/youtube-recommended-videos/)
- Some browsers may have restrictions on accessing the clipboard from bookmarklets. Ensure your browser allows clipboard access for JavaScript.

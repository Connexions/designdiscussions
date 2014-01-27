Authoring Client and Repo Design
=================================

Publishing Validations
----------------------

- Roles - validated using cnx-user
- Role Requests is stored in cnx-user
- Roles are stored in Archive after publication
- License - acceptance is stored in Archive.  Archive API will be expanded to make it available
- Module links - published and unpublished
- Links to files - these are Files that are linked to in a module
- Resources - links to images need to be validated
- User is a published or author for this content - stored in Archive.  Archive API will need to be expanded to access this

Metadata Editing Design
-----------------------

- https://github.com/oerpub/github-bookeditor/issues/157
- https://github.com/oerpub/github-bookeditor/issues/139
- https://github.com/oerpub/github-bookeditor/issues/156
- Test layout of editing buttons and access to module editing

About Us/Help Design
--------------------

- Create a collection for help pages
- The collection will be displayed in a different format from a regular collection when Help is selected
- Help will be searchable like other content
- PDF and EPUB of help will be available for download
- About Us should be one module
- About Us module will be displayed when About Us is selected 

Publishing UI
-------------

- Mockup from Kathi - http://mountainbunker.org/~maxwell/oerpub/editor-ideas/w-editor-12.html#
- Use a modal overlay
- Display a tree of modified or new items with the item currently being edited checked
- If the user selects a collection with unpublished modules, the modules should be checked
- Modal would remain until publish is completed

Derived Copies
--------------

- Collections
  - Pull TOC from archive
  - Pull modules as they are edited
- Modules
  - Pull module from Archive
  - On publish, warn user that it is a derived copy and not the original
- Collection - send changes
- Module - send module

License API
-----------

- GET license on existing content /publications/{id}/license/{user-id} returns 200 Ok.
- GET license for content that needs license acceptance /publications/{id}/license/{user-id} returns 400 Bad Request.
- POST license for content that needs license acceptance /publications/{id}/license/{user-id} accepts license and returns 200 Ok.

Roles API
---------

- GET accept role on publication at /publications/{id}/roles/{role-id} returns 200 Ok.
- Only validate on new role requests. Editor will somehow know who the original editor was. original authors will be added to json.
- If an original author is removed and added back, do not do a new role request (nice to have)

Publishing Status API
---------------------

- GET status on content being worked on /publications/{id} returns 202 Accepted with processing message.
- GET status on content that failed validation or license not accepted on /publications/{id} returns 400 Bad Request.
- GET status on content that needs license acceptance on /publications/{id} returns 202 Accepted with url to license.
- GET status on successful publicaton on /publication/{id} returns 302 Found with url to /contents/{ident-hash}

Publish API
-----------

POST data - roles, license url, url to epub
- POST new content to /contents/ accepts epub payload and returns 302 Found to /publications/{id}.
- POST content to /contents/{uuid} accepts epub payload and returns 302 Found to /publications/{id}.

EPUB Resources
- https://github.com/philschatz/epub-anatomy
- https://github.com/philschatz/books










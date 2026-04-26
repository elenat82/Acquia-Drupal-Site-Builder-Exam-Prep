# Possibili domande
> 01 You need to create an event content type that includes an event date, a location, and an image. Which Drupal feature should you use to add these fields?
- A) Manage Display
- B) Manage Fields ✅
- C) Manage Form Display
- D) Taxonomy


> 02 You have a "Category" taxonomy that must be selectable when creating a blog post. How do you link it tothe Blog content type?
- A) Enable Menu settings
- B) Add an Entity Reference field referencing taxonomy terms ✅
- C) Create a custom block with taxonomy terms
- D) Use a View to attach taxonomy terms


> 03 Your tennis club would like to publish details about events. Ech event needs a title, description, scheduled date, image, and contact information. This content will need to be searchable, sortable, and displayed in multiple formats on the site. How do you structure this content to meet the requirements?
- A) Create a custom content type called 'Event' with fields for each discreet data element ✅
- B) Create custom content types for each field and add a taxonomy term reference with common event name terms to link the nodes
- C) Use the Article content type to publish event data in the body field and group these nodes under a custom menu called 'Events'
- D) Create a custom content type called Event with the title and body fields; use the blocks to display date, image and contact information


> 04 You wish to collect users' social profile links every time they comment on a blog post. You wish to collect this only on the blog post comments; comments on other content types should not collect this information. How can you make this possible?
- A) In the blog post content type's "Manage form display" section, go to the settings for the "Comment" field and select "collect social profile information"
- B) Create a custom comment type with the appropriate custom fields for collecting social profile links. Add a Comments field to the blog post content type, making sure it uses your new custom comment type ✅
- C) Add custom fields for collecting social profile links to the default comment type
- D) Custom comment types per content type are not supported in Drupal


> 05 You run a site that attracts almost all of its users from France, even though you created the site in Australia. A number of users have started to complain that content publication times do not match their local time. Which two solutions allow users to view content in their local timezone?
- A) Alter the default timezone to that of your target audience ✅
- B) Check the "Users may set their own time zone" option in the Regional settings menu ✅
- C) Configure the content types to use France's timezone by default
- D) Set the default country to France


> 06 Your website has a content type with a Media reference field. While adding content for this content type, you wish to disallow adding files with .gif extension. How can you make this possible?
- a) Edit the Content type and disallow .gif extension in the Media reference field setting
- B) Edit the Content type and update Media field settings in Manage form display tab
- C) Edit the Media type and update field settings in the Manage display tab
- D) Edit the Media type and update media type settings to disallow .gif files ✅


> 07 You wish to implement a "star of the month" block into your company's website. The block should show name and picture of the employee and should be editable in the normal block layout interface. All the employee are users of the website. How do you implement the block?
- A) Create a user view mode with user name and picture. Add a user reference field to one of your block types and let the user reference field use the new user view mode ✅
- B) Create a new Users View with user name field and user picture and an exposed filter on uid. Add a block display to the view and place the block in the block layout
- C) Add a custom block and select the type "user account information", activate the user name and picture fields
- D) Install the user_blocks module from Drupal.org, select the fields you need and place block via block layout


> 08 On a rich media website, you wish to store the image description along with the image file while adding images to the content. You wish to reuse the images on other pieces of content as well. Which two solutions will allow you to build the functionality to store image descriptions along with images?
- A) Add a description field to the pre-existing image media type. Use the media reference field to link this with content ✅
- B) Create a media type with an image and the description field. Use the media reference field to link this with the content ✅
- C) Create a content type which will have an image and description field, and link to any content using the entity reference
- D) Search for the contributed module for adding image descriptions, as Drupal can't provide this feature out of the box
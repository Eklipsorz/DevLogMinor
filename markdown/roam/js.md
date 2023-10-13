- {{[[roam/js]]}}
    - ### ```javascript
window.importMetaDataWithoutBracket = function (item, pdfs, notes) {
const metadata = [];

  // Data that is always present can be accessed directly, like the item's title:
  metadata.push(`Title:: ${item.data.title}`);

  // But some data might be missing, in which case you may not want to add a block at all.
  // A good pattern is to test if there is any data, with an `if` statement - then only adding a block if the condition is true:
  if (item.data.creators.length > 0) { 
    metadata.push(`Author(s):: ${zoteroRoam.getItemCreators(item, { return_as: "string", brackets: false, use_type: true })}`);
  }

  // And so on. For example, not all items have an abstract:
	if (item.data.abstractNote) { 
    metadata.push(`Abstract:: ${item.data.abstractNote}`); 
  }
  // But all have a type:
	metadata.push(`Type:: ${zoteroRoam.getItemType(item, { brackets: false })}`);

  // Starting with v0.7, your custom function will now receive the item's linked PDFs, notes, and annotations,
  // without requiring you to explicitly ask for them.
  // You have access to their full metadata, and helpers that can format it for you.
  // As above, it is recommended to test for the presence of any linked content before adding Roam blocks:
	if (pdfs.length > 0) {
		metadata.push(`PDF links : ${zoteroRoam.formatPDFs(pdfs, "links").join(", ")}`);
	}
	if (notes.length > 0) {
		metadata.push({
			string: "[[Notes]]",
			children: zoteroRoam.formatNotes(notes)
		});
	}

  if (item.data.url.length > 0) {
    metadata.push(`Source:: ${item.data.url}`)
  }

  if (item.links) {
    metadata.push(`Zotero link:: ${zoteroRoam.getItemLink(item, "local")}`)
  }

	return metadata;
}```
- tags: [[Settings]]

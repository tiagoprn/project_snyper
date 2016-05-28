# MARKEE

This bullet can be used to store/retrieve links on a mongo db collection, with support
for tags. 

A link will have the following data: 
- created_at
- created_by 
- url
- tags (names)

A tag will have the following data: 
- name
- creation_date


# Requirements: 

- It must support passing a single or a list of links to be persisted. For
  simplicity, it will not be possible to add tags when a link is created. They
can otherwise be added after a successful insertion. 
 
## I must be able to retrieve:
- list of links (ordered by created_at)
- list of tags (ordered alphabetically)
- list of all the links on a single of multiple tags 

## Validations: 
- links: Should not allow creating/updating  duplicated urls;
- tags: Should not allow creating/updating duplicated names;
(IMPORTANT: the validations above and all others created 
must be tests on py.test also).

IMPORTANT: otherwise not informed, I must bring the links ordered by
created_at (most recent ones first). 

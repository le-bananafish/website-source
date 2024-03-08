# Action Plan

## Roadmap

> As at Friday 8 March, 2024 -- 19:22 [am]

"`[stable]`" features

- [x] update theme
  - [x] have post titles appear in the title bar instead of only the site name
  - [x] fix oversight whereby underlines do not wrap on homepage due to `block` vs `inline` behaviour (wrapped with `<li>`'s)
  - [x] fix lists not rendering markers
  - [x] fix homepage splash clipping into left when viewport is too small (restore deleted theme behaviour)
- [x] sort tags alphabetically
- [x] add ability to have page descriptions, archived pages, title prefixes (archive, draft, edit)
- [ ] modify the styling of certain elements, e.g. blockquotes, horizontal rules
  - [x] blockquotes
  - [x] code blocks
  - [x] horizontal rules (header/footer, article)
  - [x] fix tags being capital case, [1] (use sitewide config)
  - [x] simulate bold and italic styles
- [x] configure fonts through config.toml

"`[beta+]`" features

- [ ] build a sitewide gallery that supports filtering images so that posts can have subset galleries

"`[beta]`" features

- [ ] automatically generate a table of contents for longer posts
- [ ] automatically generate a return to top button for longer posts

## Task List

goals

- support filterable galleries so that posts can have gallery subsets but there can also be a sitewide gallery
- auto generated navigation elements (table of contents, return to top)
- tags sorted by name, posts sorted by date
- do I want descriptions?
- parameter-based prefixes on page/post titles (archive, edit, draft)

things to fix / add / improve

- [ ] modify the styling of some elements, e.g. blockquotes, line rules
- [ ] add a automatically generated `new` *floating* “return to top” button if the post is too long (I did test this out)
- [ ] make the tags page more informative, right now it’s just a list
- [ ] make lists in general show more detail and be better structured
- [ ] auto generate a nice collapsible table of contents for longer posts
- [ ] allow the user/me to change fonts (the theme hardcodes the font atm)
- [ ] fix Twitter & OpenGraph cards not rendering per post due to use of Hugo internal template which just parrots basic site information
- [ ] fix "_internal/google_analytics_async.html is no longer supported by Google"
- [ ] clean up new templating work, leverage `define`(s) and delineate what goes in `_default` vs specific bundle (page, tags)

things done

- [x] update theme version?
- [x] remove all obsolete files e.g. tags that no longer exist (done at last post)
- [x] `update` fix underlines on homepage not wrapping with text (issue is that links are being treated as blocks instead of inline, treat them as invisible `li`(s))
- [x] `update` fix lists not rendering markers (e.g. - or *) [use list-style or :before]
- [x] on homepage, splash aligns to left, clipping into left [use width:90% to fix]
- [x] have post titles appear in the title bar instead of just the site name (fixed through update)

Thanks for coming to my TED talk.

----

progress

- I've figured out how to make lists show descriptions and how to get tags to appear on post lists, the next step is to figure out how to define different behaviour for posts and tags
- I've figured out how to give posts and tags different behaviour, just define separate templates for each page bundle (e.g. /layouts/posts & /layouts/tags)
- because the links on the homepage are directly within a <nav> flex-container, they are forced to be blocks instead of inline and as such they cannot wrap. the question is how to solve the problem

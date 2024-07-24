# 👀 Reference

## Reference <a href="#reference" id="reference"></a>

This page is intended to document the themes and modules that are built into SiteBuilder, to help you reference those IDs in your own modules and build onto that content.

If you want the community to collaborate with you on what you build, we suggest you make similar documentation of your own!

#### Themes Reference <a href="#themes-reference" id="themes-reference"></a>

| Theme                     | ID         |
| ------------------------- | ---------- |
| Flowbite                  | theme\_01  |
| Flowbite Pro              | theme\_111 |
| Bootstrap 5 Design System | theme\_113 |

#### Modules Reference <a href="#modules-reference" id="modules-reference"></a>

| Module            | ID         | Submodules                                                                           | Submodule IDs    |
| ----------------- | ---------- | ------------------------------------------------------------------------------------ | ---------------- |
| Menu              | module\_2  | Headers, Footers, Sidebars                                                           | 1, 2, 3          |
| Blog              | module\_3  | Default                                                                              | 0                |
| Events            | module\_12 | Default                                                                              | 0                |
| Slider            | module\_4  | Default                                                                              | 0                |
| FAQ               | module\_10 | Default                                                                              | 0                |
| Testimonials      | module\_8  | Default                                                                              | 0                |
| eCommerce         | module\_14 | Product List, Product Detail, Cart, Order Detail, Currency Changer, Tax Code Changer | 1, 2, 3, 4, 5, 6 |
| Forms             | module\_s1 | Default                                                                              | 0                |
| Secure Zones      | module\_5  | Login Forms, Logout Buttons, User Form Submissions                                   | 1, 2, 3          |
| Pagination        | module\_s2 | Default                                                                              | 0                |
| Form Confirmation | module\_s3 | Default                                                                              | 0                |

If a module that has no sub-modules is given a sub-module in an update, the sub\_module 0 which was previously default will be renamed to miscellaneous. Layouts referencing that sub\_module will be displayed in the miscellaneous group until they are updated to reference one of the new sub\_modules.

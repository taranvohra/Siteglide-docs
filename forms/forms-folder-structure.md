# Forms Folder Structure

```
// Some code
```

#### marketplace\_builder Directory Structure

* **custom\_model\_types**
  * **forms**
    * `form_3.yml`: Configuration file for form 3.
* **form\_configurations**
  * **forms**
    * `form_3.liquid`: Liquid template for form 3's configuration.
* **notifications**
  * **email\_notifications**
    * **forms**
      * **form\_3**
        * **fic**
          * `0.liquid`, `1.liquid`: Templates for form 3 email notifications.
* **views**
  * **partials**
    * **layouts**
      * **forms**
        * **form\_3**
          * `default.liquid`: Default layout for form 3.
      * **form\_confirmation**
        * `default.liquid`: Default layout for form confirmation.
    * **tables**
      * **forms**
        * `3.liquid`: Table view template for form 3.

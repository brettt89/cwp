# 2.1.0

## Overview

We are happy to announce the 2.1.0 quarterly release of the CWP recipe.

This upgrade includes CMS and Framework version 4.2.0

 * [SilverStripe 4.2.0](https://docs.silverstripe.org/en/4/changelogs/4.2.0)

Upgrade to Recipe 2.1.0 is optional, but is recommended for all CWP sites currently on CWP 2.0.0 or above.

It contains new features which help you make decisions on an upgrade path (via the Installed Modules Report), as well as important changes to make caching of your sites safer and easier. As part of the caching changes, we’ve deprecated the (optional) [controllerpolicy module](https://github.com/silverstripe/silverstripe-controllerpolicy), and recommend new core APIs for sending HTTP cache headers instead. If you are not caching your site, this is a great time to start: Fast sites make happy users, and are more resilient to traffic spikes. Read our [CWP Performance Guide](https://www.cwp.govt.nz/developer-docs/en/2/performance_guide/) for details.

If your site is currently on CWP 1.x and you wish to upgrade, you can see what’s involved in our [Upgrading to CWP 2.0 resource](https://www.cwp.govt.nz/assets/Brochures/Upgrading-to-CWP-2.0.pdf). More information on upgrading major versions of CWP can be found in the [online documentation](https://www.cwp.govt.nz/developer-docs/en/2/working_with_projects/upgrading/).

## New Features

### Installed Modules Report

Developed for the Common Web Platform as a co-fund submission, the Installed Modules Report otherwise named in the submission as the ‘Site Summariser’ has been built to provide agencies with access to module information, allowing them to make faster and more informed decisions about upgrading their site and modules. 

Bringing site and module information to the CMS, the Installed Modules Report aims to:

* Provide those responsible for agency sites to access a snapshot on the current build of their site and what upgrades are available.
* Provide a list of what modules are utilised by the site and where further information can be found relating to user help documentation and module features.
* Highlight known module security issues.
* Provide a ‘health’ rating of each module based on the security and build quality.

The Installed Modules report can be added to your site through the combination of the below repositories. Consult with your development team to have this added to your site.

* [SilverStripe maintenance module](https://addons.silverstripe.org/add-ons/bringyourownideas/silverstripe-maintenance)
* [SilverStripe composer security checker](https://addons.silverstripe.org/add-ons/bringyourownideas/silverstripe-composer-security-checker)
* [SilverStripe composer update checker](https://addons.silverstripe.org/add-ons/bringyourownideas/silverstripe-composer-update-checker)

Information on accessing the report is covered in this [user guide](https://github.com/bringyourownideas/silverstripe-maintenance/blob/1/docs/en/userguide/index.md).

### Page History Viewer

The CWP 2.0 release [introduced content blocks](https://www.cwp.govt.nz/updates/news/cwp-2-0-release/) through the silverstripe-elemental module. This release builds on that functionality by introducing a feature developed as a co-fund submission that focuses on improving the page history viewer.

With a need for CMS users to confidently and accurately understand what has changed on a page that utilises content blocks, improvements have been made to allow users to review the edit history of both the content blocks as individual components as well as a group of content blocks sitting on a particular page.

This improvement allows content blocks to be auditable and supports compliance with Official Information Act requests and Information and Records Management standards.

### Caching Improvements

HTTP caching is an important part of making websites fast and reliable. This CWP release aims to avoid mistakes in the process by providing more high level [HTTP Caching APIs](https://docs.silverstripe.org/en/4/changelogs/4.2.0/#http-cache-header-changes). The default system behaviour will also pick up more situations where caching needs to be disabled automatically, for example when previewing draft content. CWP projects can choose to make this behaviour more secure by opting out of [session-based draft stages](https://docs.silverstripe.org/en/4/changelogs/4.2.0/#disable-session-based-stage-setting) and solely relying on the `?stage=Stage` parameter.

## Security Changes

* Resolved a potential SQL injection exploit in the silverstripe-subsites module. While it was not likely to be exploitable, the issue has been mitigated. See [SS-2018-016](https://www.silverstripe.org/download/security-releases/ss-2018-016).

For details on these and previous security fixes, please refer to our [security release announcement page](http://www.silverstripe.org/software/download/security-releases/).

## Upgrading Instructions

This upgrade can be carried out by any development team familiar with SilverStripe CMS, but if would like
SilverStripe's assistance, you can request support via the [Service Desk](https://www.cwp.govt.nz/service-desk/new-request/).

In order to update an existing site to use the new recipe the following changes to your composer.json can be made:

```
"require": {
    "php": ">=5.6.0",
    "silverstripe/recipe-plugin": "^1",
    "cwp/cwp-recipe-core": "2.1.0@stable",
    "cwp/cwp-recipe-cms": "2.1.0@stable",
    "silverstripe/recipe-blog": "1.1.0@stable",
    "silverstripe/recipe-form-building": "1.1.0@stable",
    "silverstripe/recipe-authoring-tools": "1.1.0@stable",
    "silverstripe/recipe-collaboration": "1.1.0@stable",
    "silverstripe/recipe-reporting-tools": "1.1.0@stable",
    "cwp/cwp-recipe-search": "2.1.0@stable",
    "silverstripe/recipe-services": "1.1.0@stable",
    "silverstripe/subsites": "2.1.0@stable",
    "tractorcow/silverstripe-fluent": "4.1.3@stable",
    "silverstripe/registry": "2.1.0@stable",
    "cwp/starter-theme": "2.0.1@stable"
},
```

Inclusion of the new Installed Module Report, mentioned above, requires both the above upgrade step as well as the separate recipe requirement silverstripe/recipe-reporting-tools 1.1.0. This recipe is included by default with CWP 2.1.0 installations, however if you are upgrading you will need to update your constraint to 2.1.0.

A stable version of `silverstripe/textextraction` (3.0.0) is now available for use in CWP 2.1.

## Other Notable changes

 * The default project name has been changed from `mysite` to `app`
 * Disable session-based stage setting in `Versioned`
 * Versioned cache segmentation by stage

## Accepted Failing Tests

All noted failures have been fixed and will be resolved in the next CWP 2.1 or 2.x recipe release.

### recipe-cms

 * SilverStripe\AssetAdmin\Tests\Controller\AssetAdminTest::testSaveOrPublish ([issue](https://github.com/silverstripe/silverstripe-asset-admin/issues/787))
 * SilverStripe\CMS\Tests\Model\SiteTreeTest::testCanEditWithAccessToAllSections ([issue](https://github.com/silverstripe/silverstripe-cms/issues/2178))
 * SilverStripe\CMS\Tests\Model\SiteTreeTest::testCanPublish ([issue](https://github.com/silverstripe/silverstripe-cms/issues/2178))
 * SilverStripe\AssetAdmin\Tests\Forms\FileFormBuilderTest::testCreateFileForm: affected by global state
 * SilverStripe\AssetAdmin\Tests\GraphQL\FolderTypeCreatorTest::testItDoesNotFilterByParentIdWithRecursiveFlag: affected by global state
 * SilverStripe\AssetAdmin\Tests\Forms\RemoteFileFormFactoryTest::testRejectedURLS: affected by global state

### recipe-content-blocks

 * DNADesign\Elemental\Tests\ElementalAreaTest::testCanBePublished: Affected by global state

### recipe-services

 * SilverStripe\VersionFeed\Tests\VersionFeedTest::testRateLimiting

<!--- Changes below this line will be automatically regenerated -->

## Change Log

### Security

 * 2018-07-15 [4b6804e](https://github.com/silverstripe/silverstripe-subsites/commit/4b6804eaabe26516069ca16063b9bef45107d9f3) Group table name is escaped to prevent possibility of SQL injection (Robbie Averill) - See [ss-2018-016](https://www.silverstripe.org/download/security-releases/ss-2018-016)

### API Changes

 * 2018-06-27 [21f8463](https://github.com/silverstripe/cwp-core/commit/21f8463e1e7fe8e0798f06ecb98f4d60da5de4a7) Removed CwpCanonicalURLMiddleware in favour of core CanonicalURLMiddleware (Robbie Averill)
 * 2018-03-21 [100be38](https://github.com/silverstripe/silverstripe-userforms/commit/100be38ab1df82f411243e4213794b7974672b64) Remove use of getEscapedTitle() and deprecated for future removal. Use $Title directly instead. (Robbie Averill)

### Features and Enhancements

 * 2018-06-19 [21f4d80](https://github.com/silverstripe/silverstripe-subsites/commit/21f4d80ef2027ba9d58fe15e9a2498299097419f) Hide subsite selector dropdown if no subsites have been created yet (Robbie Averill)
 * 2018-06-17 [42d24df](https://github.com/silverstripe/silverstripe-spellcheck/commit/42d24df8e730c9db4761fcd67c7643b0a7e0fd3d) Lazy-load spellcheck config instead of every request (Damian Mooyman)
 * 2018-06-12 [92d1445](https://github.com/silverstripe/recipe-reporting-tools/commit/92d144597873b8c61ba0397a5ac9b836bfd30bf6) Adding silverstripe-maintenance report (Guy)
 * 2018-05-29 [987798f](https://github.com/silverstripe/cwp/commit/987798f11785471adf34663240b441917d8fb808) Adding extension for relabelling filter options on report (Guy)
 * 2018-05-02 [b205ca9](https://github.com/silverstripe/silverstripe-userforms/commit/b205ca952a8ff29e5b0e1e8baffde3181bf8a155) default value for Country Dropdown (add i18n to the new fields) (Chen Shenghan)
 * 2018-05-01 [8870833](https://github.com/silverstripe/silverstripe-userforms/commit/887083331875b8b68f9d8cf5c9bef8fd42b277fe) empty default value for Country Dropdown (Chen Shenghan)
 * 2018-04-29 [4d89705](https://github.com/silverstripe/silverstripe-userforms/commit/4d89705fe6fbb37274c4f222ecb01894022c831b) default value for Country Dropdown (Chen Shenghan)
 * 2018-04-26 [e2035ad](https://github.com/tractorcow/silverstripe-fluent/commit/e2035ad054f543b2137a46a244f1afa4f8dfc33b) Shift extension default to yml file to promote better extensibility (Damian Mooyman)
 * 2018-04-22 [350a9c4](https://github.com/tractorcow/silverstripe-fluent/commit/350a9c427235842b310b79837f8a94270d782549) Allow frontend publish filter to be disabled via yml (Damian Mooyman)
 * 2018-04-05 [9d26cff](https://github.com/silverstripe/silverstripe-blog/commit/9d26cff23d8a4c047321f701ea32d818e58b9891) Add translation support for blog post authors profile summary heading (Robbie Averill)

### Bugfixes

 * 2018-07-25 [65464f0](https://github.com/silverstripe/cwp-core/commit/65464f02e30ec5ef7896e7deb69e4b63b55ebb0f) LoginAttemptNotifications extension is now disabled again, as it is in CWP 1.x (Robbie Averill)
 * 2018-07-04 [5370bc8](https://github.com/silverstripe/silverstripe-subsites/commit/5370bc8af68646634396a9d13202b39b6c3719b2) apply SubsiteID getVar to CMS Preview fetches (Dylan Wagstaff)
 * 2018-07-02 [c0a01db](https://github.com/silverstripe/silverstripe-comments/commit/c0a01dbc91ace606e3cc5ab6fa0e16c6dd41b9aa) created way of knowing whether user has permission to post (micmania1)
 * 2018-06-29 [edec1d7](https://github.com/symbiote/silverstripe-advancedworkflow/commit/edec1d70f1812ad13e71e183e18f303e184484b9) Admin users can always edit records that have active workflow transitions (Robbie Averill)
 * 2018-06-29 [ea42a8d](https://github.com/silverstripe/cwp/commit/ea42a8d9d90356822b4aba7f053961e107489af3) Maintenance module configuration for CWP is now in place (Robbie Averill)
 * 2018-06-28 [d96f52c](https://github.com/symbiote/silverstripe-advancedworkflow/commit/d96f52cc358722498e948d4d7e25e27cd631ffe5) Email notification workflow now ignores recipients with invalid email addresses (Robbie Averill)
 * 2018-06-28 [0056ef3](https://github.com/symbiote/silverstripe-advancedworkflow/commit/0056ef3d69058b18b1a737dac680b26e4240ee2c) Make template optional for workflow definition (Raissa North)
 * 2018-06-28 [1f4ad99](https://github.com/symbiote/silverstripe-advancedworkflow/commit/1f4ad999f485b8bc9083ea832d34c44d2ea18576) Update Reminder Email DB Field mismatch to ensure value saves (Raissa North)
 * 2018-06-27 [fb446b6](https://github.com/silverstripe/silverstripe-fulltextsearch/commit/fb446b613f1ce0c343c10303302be7469ef045ca) Reduce log level so errors do not automatically output (Guy)
 * 2018-06-27 [97891b5](https://github.com/silverstripe/silverstripe-fulltextsearch/commit/97891b5fa393eebbe4b62427cbf1f9f2b27f2752) ing linting issue that couldn't be automatically resolved (Guy)
 * 2018-06-27 [5c12baa](https://github.com/silverstripe/silverstripe-fulltextsearch/commit/5c12baaaa9dde6e3ae26eb015f4d2b8bea82b1ec) Use \Exception for catching Solr exceptions (Guy)
 * 2018-06-27 [4e25f5f](https://github.com/silverstripe/cwp/commit/4e25f5f93c1bca7abcf79880a9da7632b83f6556) Remove COMPOSER_HOME definition, update-checker module now does this itself (Robbie Averill)
 * 2018-06-26 [837920a](https://github.com/silverstripe/cwp/commit/837920a6bd00d190444c70fb69f6566d1d02f975) Maintenance module extension now provides CWP proxy information for HTTP requests (Robbie Averill)
 * 2018-06-20 [a2af250](https://github.com/symbiote/silverstripe-queuedjobs/commit/a2af250bb7fac32952e7b2358022933f99b0e4bb) Allow integration/unit tests to use more memory, update assertions and docblock tweaks (Robbie Averill)
 * 2018-06-20 [6c56694](https://github.com/silverstripe/silverstripe-contentreview/commit/6c56694bdedda733020298d96d48b432f20e29ad) Update modal API for Reactstrap in SilverStripe 4.2, bump constraint (Robbie Averill)
 * 2018-06-20 [c7235e1](https://github.com/silverstripe/silverstripe-comments/commit/c7235e1c5d092e041b2956673fb2870665560184) Comments GridField tests now use their own test stubs (Robbie Averill)
 * 2018-06-20 [886c5be](https://github.com/silverstripe/silverstripe-comments/commit/886c5be21aad47198630daee4e8cb3325fd74421) Bug with requiring login when posting a comment, pass correct controller in (Robbie Averill)
 * 2018-06-19 [d392ca7](https://github.com/silverstripe/silverstripe-blog/commit/d392ca72f19e607f69973f635b559229c61d337a) Make sure `setAllowMultibyte` is on when looking up by URLSegment (Daniel Hensby)
 * 2018-06-19 [dc9d6de](https://github.com/silverstripe/silverstripe-subsites/commit/dc9d6de62dbea4d14d7b8e3b7d6b7ca01d7674e9) Do no provide input for canEdit or canPublish if no subsites exist (Robbie Averill)
 * 2018-06-19 [3156218](https://github.com/silverstripe/silverstripe-subsites/commit/315621892d2f6bec914fba8a03ea996973d25209) Double escaping subsites title in CMS menu (Robbie Averill)
 * 2018-06-18 [6f37490](https://github.com/silverstripe/cwp/commit/6f3749042f1ddc26907919e036ad50703d7695c9) Use correct TinyMCE skin in CWP CMS instances, remove closure scope (unneeded) (Robbie Averill)
 * 2018-06-18 [279b67d](https://github.com/tractorcow/silverstripe-fluent/commit/279b67d1722ee9393409e25018f59811a39257ba) Only force change for written records when not in current locale, or not versioned (Robbie Averill)
 * 2018-06-18 [9abfaf7](https://github.com/silverstripe/cwp-recipe-cms/commit/9abfaf7abab3e4a82487dab1158d8e47f1b0cb79) Add proxy configuration for embedded cURL requests (Robbie Averill)
 * 2018-06-18 [d989074](https://github.com/symbiote/silverstripe-queuedjobs/commit/d989074f4049239a59b3e368f501259b8f35c4cf) ed a case where original user was missing when unsetting a user. (Mojmir Fendek)
 * 2018-06-17 [a6aa171](https://github.com/silverstripe/silverstripe-sitewidecontent-report/commit/a6aa1714d6c9e7f34eb31095e76a149bd0097522) Replace recipe-cms requirement with CMS module (Robbie Averill)
 * 2018-06-15 [32ec3bd](https://github.com/silverstripe/silverstripe-comments/commit/32ec3bde50f3fa63a0a9ff4ab474052695276734) Add getDate method to return created date for comments, tidy up translations (Robbie Averill)
 * 2018-06-15 [788cb6e](https://github.com/silverstripe/silverstripe-comments/commit/788cb6e6d186fad7ab42aa6bb42ed5b352eaf4e8) Mock akismet spam protector if installed, fixes broken integration tests (Robbie Averill)
 * 2018-06-15 [fc36eac](https://github.com/silverstripe/silverstripe-fulltextsearch/commit/fc36eac3b3d4bc3b4d7c42b497f165b4ce623b75) Remove method clearing dummy data from test fixture methods, DB rollbacks do this already (Robbie Averill)
 * 2018-06-15 [2fdf87b](https://github.com/silverstripe/silverstripe-fulltextsearch/commit/2fdf87bbf1f70f044d23e4d4688c417bebab9ddf) Remove resetDBSchema use, not required and breaking 4.2 tests (Robbie Averill)
 * 2018-06-14 [b653758](https://github.com/silverstripe/silverstripe-fulltextsearch/commit/b653758c8033ca5fb72a2bc982ae552c7b9b26fa) Fix psr-4 namespace errors due to incorrect case (Damian Mooyman)
 * 2018-06-12 [eca3ac0](https://github.com/silverstripe/silverstripe-comments/commit/eca3ac0e94f809e8cb4cc3b60d394b2a88faddae) Allow tests to handle extra field labels being added in global state (Robbie Averill)
 * 2018-06-12 [40c283a](https://github.com/silverstripe/cwp-starter-theme/commit/40c283aad1b972544edb661151cff381ee44c6ba) Update SelectionGroup template to correctly render selected classes (Robbie Averill)
 * 2018-06-07 [10c209c](https://github.com/tractorcow/silverstripe-fluent/commit/10c209c5756abe7d1d1e19b3d74e80218018fe5b) Don't fail on empty locale (Damian Mooyman)
 * 2018-06-06 [e02691a](https://github.com/tractorcow/silverstripe-fluent/commit/e02691ad276e6d31ce95fb20126a130b742e8cc7) Fix invalid locale being set for domain mode (Damian Mooyman)
 * 2018-06-06 [2463ca2](https://github.com/silverstripe/cwp/commit/2463ca213b004e670e7f790077627c3362302839) broken links in docs (#95) (Raissa North)
 * 2018-06-05 [9e923d6](https://github.com/silverstripe/silverstripe-restfulserver/commit/9e923d6f9e33c5ff07f5144daa46e0dcb720e159) Fixes #65 Use Injector to instantiate created objects. (#68) (Russ Michell)
 * 2018-06-01 [5b47edc](https://github.com/silverstripe/cwp/commit/5b47edc5416cf8a4c8b1b9e2b6bea4bd50f0fb17) broken links (#94) (Raissa North)
 * 2018-06-01 [cc6005d](https://github.com/silverstripe/silverstripe-userforms/commit/cc6005d81dda09db021292d55b4503ceca2cf72d) Disable themes in UDF functional test. Fixes failure with cwp/starter-theme (Robbie Averill)
 * 2018-06-01 [ce1db58](https://github.com/silverstripe/cwp/commit/ce1db58045b6b1cfcfda8cc2ef7d88d1a3e0f17d) broken link (#92) (Raissa North)
 * 2018-06-01 [1012ccb](https://github.com/silverstripe/cwp/commit/1012ccbb4c231caae30faa398c4aca935c5a3048) broken link (Raissa North)
 * 2018-06-01 [af89140](https://github.com/silverstripe/cwp/commit/af8914063d3a3a8298ef6c3936f72ddd51d7174d) broken link in developer docs (#91) (Raissa North)
 * 2018-06-01 [af06f80](https://github.com/silverstripe/silverstripe-subsites/commit/af06f803c56756e395359ffacbfaf2e8370b93a0) Re-enable Behat using chromedriver and silverstripe/recipe-testing (Robbie Averill)
 * 2018-06-01 [8222f61](https://github.com/silverstripe/silverstripe-subsites/commit/8222f619f8465d09b8cd43b63fc5caf8d04d1757) Use correct table name for Group model when performing DB upgrades from older versions (Robbie Averill)
 * 2018-06-01 [bc2348a](https://github.com/silverstripe/cwp-starter-theme/commit/bc2348a523a5ed74f2f8a7fe98fd93c3db1ce147) Reverting Jumbotron restyle (Guy)
 * 2018-06-01 [60a98be](https://github.com/silverstripe/cwp/commit/60a98be6391ec70f7fc6c4847ed2c9f60a44686c) broken links in developer docs (Raissa North)
 * 2018-06-01 [b6ba567](https://github.com/silverstripe/silverstripe-subsites/commit/b6ba567ee5c947358fee47adaa6b4f931b000789) Do not make subsite based file permission decisions when no subsite is set (Robbie Averill)
 * 2018-05-31 [8e4fbd0](https://github.com/silverstripe/silverstripe-restfulserver/commit/8e4fbd063649bde2fda7ce5c7490403c9e28b29b) Fixes #63 Conditionally permit additional GET request in POST context. (#64) (Russ Michell)
 * 2018-05-30 [c22daa2](https://github.com/silverstripe/silverstripe-comments/commit/c22daa2ee06956eae6ee486dabb8696c6294ad51) Removing ID from match in tests (Guy)
 * 2018-05-29 [a6f9595](https://github.com/silverstripe/silverstripe-sitewidecontent-report/commit/a6f95957a0dad3ca0e4ddef28a7d21230835744c) Correct assertion order and remove default pages from Subsite creation (Robbie Averill)
 * 2018-05-29 [8fc5a6b](https://github.com/symbiote/silverstripe-queuedjobs/commit/8fc5a6b7deabb0fea6f8554ba811901b9ebda52c) Implement subsites namespace into QueuedJobService (Robbie Averill)
 * 2018-05-28 [34eb6ed](https://github.com/silverstripe/silverstripe-securityreport/commit/34eb6ed01b068034dd6b0a6b150be880ad805c30) Remove "Login Attempts" tab from Member CMS fields (Robbie Averill)
 * 2018-05-28 [2a97b05](https://github.com/symbiote/silverstripe-queuedjobs/commit/2a97b05f50bac8f7df8bfd40f4d1cfb861dd2ed4) Mock current date and time in scheduled execution test (Robbie Averill)
 * 2018-05-27 [191178c](https://github.com/symbiote/silverstripe-queuedjobs/commit/191178cbca78c8e2b6b5f75979637544970828f3) Use correct namespaces for Versioned and ErrorPage (Robbie Averill)
 * 2018-05-20 [33044ac](https://github.com/silverstripe/silverstripe-userforms/commit/33044ac91761489b6a4f9e800165c9ce3ad5d320) #759: Enable navigating to former pages via page number button in multi-page userforms. (Shenghan Chen)
 * 2018-05-18 [4913290](https://github.com/silverstripe/silverstripe-userforms/commit/491329044b38314f217e750d810ec1237451c660) Add extension to remap polymorphic relationship classes for Parent and Form fields (Robbie Averill)
 * 2018-05-09 [07ca22e](https://github.com/silverstripe/silverstripe-userforms/commit/07ca22e729d67393d312affdc9e14f6611cebe36) (SubmittedFormField): Fix bug where FormattedValue isn't cast to HTMLFragment, which causes &lt;br/&gt; to appear in Email templates. (Jake Bentvelzen)
 * 2018-05-08 [cacf25f](https://github.com/silverstripe/silverstripe-restfulserver/commit/cacf25fb9b6f00a4297ea965bad1165cb3c3f66d) infinite redirect after PUT (#62) (andreaspiening)
 * 2018-05-06 [b3cff89](https://github.com/symbiote/silverstripe-queuedjobs/commit/b3cff8990eec35917dddf79542c7001f214d4b5e) Fixes #173 Check for excistence of root object. (Russell Michell)
 * 2018-04-24 [2e18723](https://github.com/symbiote/silverstripe-queuedjobs/commit/2e18723f4cd8875313b0e8714508b7f60cd67b43) Swap deprecated Member::currentUser and check that $jobType is a job (Robbie Averill)
 * 2018-04-20 [dc26478](https://github.com/silverstripe/silverstripe-blog/commit/dc26478e94c0025379ff94ad4920c3780a9b3ffa) Use correct API for determining if record is modified on draft stage (Robbie Averill)
 * 2018-04-20 [9e6fa08](https://github.com/silverstripe/silverstripe-securityreport/commit/9e6fa085a1d9602eaa55a3689796d511c3ec7fd3) revert removal of 'last logged in' column (Dylan Wagstaff)
 * 2018-04-16 [4ec6eb4](https://github.com/silverstripe/silverstripe-restfulserver/commit/4ec6eb4db041052544539fe79c41d88a0173890f) fix JSONDataFormatter to not convert values to XML (Andreas Piening)
 * 2018-04-15 [4d333b2](https://github.com/silverstripe/silverstripe-taxonomy/commit/4d333b2a06bb5dd23fd106a56dcae892c60c6b93) Move directory controller template into correct location (Robbie Averill)
 * 2018-04-13 [478e5dc](https://github.com/silverstripe/recipe-cms/commit/478e5dc84021d45e9abc06747ab81e98d8062b89) invalid htaccess (Damian Mooyman)
 * 2018-03-28 [569b0a7](https://github.com/silverstripe/silverstripe-userforms/commit/569b0a7627a3b6818c8b7c7793bf90dd51747fa9) use the same translation variable key as core (#755) (Dylan Wagstaff)
 * 2018-03-23 [5cce5f5](https://github.com/silverstripe/silverstripe-userforms/commit/5cce5f5a17f562f0cebc8e1efb27ef7f3e63bafd) Allow editable form fields to have nullable titles rather than fallback to Name (Robbie Averill)
 * 2018-03-23 [7cbffd8](https://github.com/silverstripe/silverstripe-userforms/commit/7cbffd8c84ea09fe73d1b177e003a9e103d1c468) Use a userforms template for the member list field, fixes broken display rules (Robbie Averill)
 * 2018-03-22 [453a35e](https://github.com/silverstripe/silverstripe-userforms/commit/453a35e114cae6d1e1ab5f55a9b6764a74a09d90) Ensure duplicated multiple option field is written (has an ID) before duplicating options (Robbie Averill)
 * 2018-03-22 [86b098c](https://github.com/silverstripe/silverstripe-userforms/commit/86b098ccf5d3db3597a50d38b74b4ce81dd6d2d8) Disable versioned GridField extensions - it conflicts with UserFormRecipientItemRequest (Robbie Averill)
 * 2018-03-22 [92a2229](https://github.com/silverstripe/silverstripe-userforms/commit/92a222924948c49dfd05290965ced81d4598c876) Correctly return the max file size in MB (Robbie Averill)
 * 2018-03-20 [8868535](https://github.com/symbiote/silverstripe-queuedjobs/commit/8868535ff5449f27d039edf8f3f21934a2afa11a) Ensure null-&gt;ID is not evaluated (Gordon Anderson)
 * 2017-05-15 [f6f6731](https://github.com/symbiote/silverstripe-queuedjobs/commit/f6f67314dad8b90ca22b918de033257f189e3dcb) markStarted not calculating timeout correctly (matt-in-a-hat)
 * 2017-02-03 [3679cb7](https://github.com/silverstripe/silverstripe-contentreview/commit/3679cb7f7d35716f5309fd46fd26541009e7ee91) Ensure QueuedJob health check doesn't kill long running review jobs (Jake Bentvelzen)

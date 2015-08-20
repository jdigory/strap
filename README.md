# Strap Template for Interchange

This is a modern HTML demo for Interchange, built on the [Bootstrap Framework](http://getbootstrap.com/), version 3.x.

It uses the Bootstrap CSS and JS files from the [Bootstrap CDN](http://www.bootstrapcdn.com/).

Alternatively, you can [download a customized Bootstrap](http://getbootstrap.com/customize/), upload it to your
Document Root, and then alter the templates to use it.

[jQuery](https://jquery.com/) is also included. Both Bootstrap and
jQuery as-used support Internet Explorer 8 and above.

The Bootstrap and jQuery files are loaded from `variables/CSS` and
`variables/JS`, if you wish to update the versions used.

This program is offered without warranty of any kind. See file LICENSE
for redistribution terms.

## Requirements

Works best with Interchange version 5.8.1 or higher.

## Usage

Clone the repository (or download the ZIP file and extract, then rename
"strap-master" to "strap") to your Interchange directory (e.g.
/usr/local/interchange). From there, run:

  `bin/makecat --demotype=strap [your-catalog-name]`

Note: if you previously installed the "standard" template, you should
      first run this command:

  `rm [/path/to/interchange]/code/template_tag/standard/pay_cert*`

## Notes

* If you want stock alerting, you need to add a cronjob for the user of
  your catalog, to run the 'daily' Interchange job. Something like:

  `0 1 * * * /path/to/your/interchange/bin/interchange --runjobs=your_catalog_name=daily --quiet`

* There may be problems with UTF-8 and recent Perls. You can disable
  UTF-8 by commenting 2 lines in catalog.cfg, under "Encoding". For
  instance, this is a known issue with UTF-8 enabled:
  	https://github.com/interchange/interchange/issues/84
  If disabling, set an environment variable of `MINIVEND_DISABLE_UTF8` to `1`

## Some of the changes include

* Product Groups and Categories use the "ncheck" subroutine in
  catalog.cfg to allow pretty, SEO-friendly URLs, such as `/Tools/Hand-Saws`

* SEO-friendly "more" paging: no more unindexable "more" pages, nor need
  to use PermanentMore. Now, "more" pages are: `/2`, `/3`, `/Next`,
  `/Previous`. Also provides canonical and "rel=prev/next" meta tags.

* All links no longer include '.html'. Configured in `catalog.cfg` in
  `ScratchDefault mv_add_dot_html`.

* New link for all products: `/All-Products`

* Searches are now sent as GET requests, not POSTs. Also now uses
  SearchProfile for very short URLs -- search query is sent in the "s"
  parameter, for easy tracking via Google Analytics.

* Use of UserDB's `indirect_login` by default, to allow emails as
  usernames (uses a new 'usernick' column).

* Password Reset page no longer emails password (bad practice). Now
  sends a basic encoded link to reset the password, which expires in 1
  day. Requires installation of Bundle::Interchange CPAN module.

* Checkout pages have a ton of clean up, and improved with user-experience
  guidelines for Checkout from Baymard Institute. 

* Multi-page checkout is the default. No more ord/multi.html. The
  Shipping Address page (ord/shipping.html) now has a login prompt
  at the top.

* One-page checkout is still included and accessible from the top menu.
  However, it is only recommended if you have a shipping setup that does
  not depend on a geographical location; if your shipping changes
  based on country/state/ZIP, etc, it will not refresh the page to
  obtain the correct rates. Javascript-based page refreshing is not
  reliable with modern browers and their auto-fill functions.

* Gift certificates (pay certs) supported out-of-the-box. Several code
  improvements, including ability to validate certificate's check-code
  and expiration, and ability to pay for entire order or part of order
  with a gift cert.

* Stock Alert function updated to use a database table and Job to email
  when item is back in stock.

* Address Book (`member/ship_addresses.html`, etc) and Saved Carts have
  been removed. We found these features were too complex and little-used
  in their current state.

* Admin `order_view` page updated to show `gift_note`,
  `tracking_number`, and `pay_cert` totals.

* Admin "Content" tab is hidden, since old Content Editor is not
  supported anymore.

* Basic page editor for Admin users is available to pages that include:
  `[tmpn editable]1[/tmpn]`. Login to Admin, then browse page. "Edit page
  data" button will be visible in lower-right corner.

* Page to reconfigure catalog: `pages/test/recon.html`

* Page to show shipping information: `pages/test/ship.html`

* Error Log now lives in `logs/` directory, instead of catalog root.

* Consolidated `LEFTRIGHT`, `LEFTONLY`, `NOLEFT_TOP` & `NOLEFT_BOTTOM` variables into
  `variables/TOP` & `variables/BOTTOM`. Other areas, such as "CSS", are also now in
  `variables/`. Changes in templates can still be hard coded in `BOTTOM`,
  but the long-present but seldom-used `display_class` in individual
  page headers is used more often.

* Templates leftright, leftonly, noleft, formerly located in
  `include/layout` have been moved to more appropriately named
  `templates/`. This to consolidate directory structure and make
  location of templates more intuitive. Can be easily changed to be more
  backward compatible if desired by simply editing `variables/BOTTOM`

* No longer using `THEME_CSS`.

* The page title and page banner can be set anywhere before the
  page footer.

* Profiles moved from `etc/` to `include/profiles/`

* All shipping files/databases moved to `products/ship`.

* No more etc/after.cfg -- all configuration in catalog.cfg.

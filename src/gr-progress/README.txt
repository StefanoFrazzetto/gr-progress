=== GR Progress Widget ===
Contributors: cmeeren
Tags: books, goodreads, reading, reading lists
Donate link: https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=QW6S8UK8SETUN&lc=US&item_name=Donation%20to%20GR%20Progress%20Widget&currency_code=USD&bn=PP%2dDonationsBF%3abtn_donateCC_LG%2egif%3aNonHosted
Requires at least: 3.7
Tested up to: 5.0
Stable tag: trunk
License: GPLv2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html

Widget to display shelves and reading progress from Goodreads.

== Description ==

This is a "set it and forget it" widget which allows you to display shelves and reading progress from your Goodreads profile. You can add multiple widgets and configure them individually to show multiple shelves.

Some configuration options:

* Large/small cover images
* Message to display if shelf is empty
* Sort books by reading progress, date updated, shelf position, author, title, etc.
* Number of books to display
* Display your rating
* Show first line of your Goodreads review (intended for quick notes such as "reading this together with Alice", "recommended by Bob", links to reviews, or whatever else strikes you fancy)
* Show reading progress bar, progress text (no bar) or don't show progress at all
* Display time since last update (e.g. "2 days ago")
* Custom strings for time since last update (e.g. for quick and easy translating, or to change "2 days ago" to "2 floobargles since last update")

Almost all HTML elements have dedicated CSS classes to allow you to easily override the style. The widget looks OK on the most popular Wordpress themes.

Requires PHP 5.4 or later (PHP 7 supported).

The source is hosted on [GitHub](https://github.com/cmeeren/gr-progress).

== Installation ==

1. Make your Goodreads profile public (Account Settings - Settings - Who can view my profile: anyone), otherwise no books will be visible.
2. Install and activate the plugin as you normally do.
3. Go to Appearance -> Widgets and find "GR Progress". Drag it to your preferred sidebar or other widget area.
4. Go through all the widget settings and configure according to your preferences. User ID, API key, and Goodreads shelf name are mandatory. Get a Goodreads API key [here](https://www.goodreads.com/api/keys) (it doesn't matter what you write).

== Frequently Asked Questions ==

= Important performance considerations =

If you can, please use this widget with shelfs with few books (for example, less than 100 books should work fine in most cases). If you use a shelf with many books, then regardless of the "Display at most X books" setting, fetching books will take a long time because the Goodreads servers need to sort all your books before picking the X books send to the widget.

This has two important implications. Firstly, it causes a poor experience for the first visitor to your page after the GR Progress Widget cache has expired and needs to refresh, since that user will potentially be waiting a long time for your page to load. Secondly, depending on your PHP settings, it may cause timeouts causing the widget to fail and report an "Error retrieving data from Goodreads" message. (The widget currently has a hardcoded timeout setting of 30 seconds, which is shorter than most PHP installations and longer than you should find acceptable.)

If you're a somewhat advanced user, you can set the widget's cache time to 0 (infinite) and schedule an automated job (e.g. a cron job) that fetches/visits your blog with the url variable 'force_gr_progress_update' added (e.g. http://yoursite.com/page_with_gr_progress_widget/?force_gr_progress_update). If you do this, visitors to your site will never experience slow loading times due to the widget, because updates will be done solely by the cron job.

= Troubleshooting =

Before we start, let me make clear that I have made this plugin for myself and provide it free of charge in case anyone else likes it. If it doesn't work for you, there are a few things you can try, and I might be able to help you on the forum. But remember that I don't have paying customers, so don't expect me to spend much of my spare time debugging problems, particularly if I can't reproduce them myself.

* It just says "Error retrieving data from Goodreads" *

Follow the below steps:

1. Make sure you've configured it correctly. Double-check your user ID, your API key, and the shelf name. Note that the shelf name is typically something like "currently-reading", not "Currently reading".

2. Make sure your Goodreads profile really is public. Go to your Goodreads profile, copy the URL, and visit it in a browser where you are signed out of Goodreads. If you can't see your shelves and books, neither can this widget. If you make changes to your Goodreads privacy settings, make sure to re-save the widget settings before testing to reset the widget's cache.

3. If your settings are correct and your profile is publis and it still doesn't work, go to the plugin support forum and describe the error. Include the most important widget settings (user ID, API key, and shelf name). I will then be able to test your settings myself.

4. If everything works fine when I test it, there is usually little I can do for you. Note that certain webhosts have been reported to cause problems with this widget, and one user reported the widget working again after switching hosts.

= Why do I have to get my own Goodreads API key? = 
Because Goodreads doesn't allow calling any given combination of an API key and an API endpoint more than once per second. On the off-chance this plugin gets wildly popular, I don't want Goodreads shutting down my own API key due to excessive usage.

= What if I'm unable/unwilling to use my own API key? = 
Create a new Goodreads user and get an API key for that user. Doesn't matter which key you use, it just has to be a valid Goodreads API key.

= Is the Goodreads attribution really mandatory? = 
Yes, according to the Goodreads API terms of service.

= What if I style my widgets like one of the screenshots, so that the second shelf/widget appears to be part of the first widget - can I then hide the attribution on the second widget? =
My personal guess is yes, because it would be clear from the first attribution that the data in both widgets come from Goodreads. I don't make the rules, though.


== Screenshots ==
1. The plugin in action
2. The plugin with a bit of custom styling to make two widgets look like one
3. The widget settings as of version 1.0.0

== Changelog ==

= 1.5.5 =
* Fixed bug where multiple widgets with different user IDs produced the same shelves when the shelf names were identical

= 1.5.4 =
* Increased the widget timeout to 30 seconds, which should fix the "Error retrieving data from Goodreads" message some people have been seeing. Please read the new "Important performance considerations" part of the readme.

= 1.5.3 =
* Switched all Goodreads URLs to HTTPS

= 1.5.0 =
* Added support for displaying your book ratings
* Added help text explaining how Goodreads authors can find their user ID

= 1.4.1 =
* Fixed bug where any error in fetching data from Goodreads would disable
  all future fetching until the widget settings were re-saved.

= 1.4.0 =
* You can now force updates by adding 'force_gr_progress_update' as a url variable (e.g. by visiting http://yoursite.com/page_with_gr_progress_widget/?force_gr_progress_update).  This can be automated e.g. using cron jobs if your host supports it. Combined with setting cache time to 0 (infinite), visitors to your site will never experience slow loading times due to the widget having to fetch data from Goodreads.

= 1.3.0 =
* Cover images now use the same protocol (http or https) as the rest of the page

= 1.2.0 =
* Allow links in book titles and Goodreads attribution

= 1.1.0 =
* Synchronize multiple widgets so that they all fetch data at the same time (to avoid books being shown in more than one shelf if it is moved on Goodreads). The shortest cache time will be used.

= 1.0.1 =
* Fix bug which made plugin appear twice in the Plugins list.

= 1.0.0 =
* Initial release.

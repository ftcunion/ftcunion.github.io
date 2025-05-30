# Static website backup

![website files downloading with wget](./screenshot.svg)

This is a simple script that scrapes the website using `wget` in order to maintain a static fallback. This script requires pretty permalinks unless used on a single page site.

The script runs three download steps:

1. Download all files on the website using `wget`, waiting 1 second between requests. The script ignores any file with a query parameter unless that parameter is `?ver`.
2. Download the website's 404 page. This fails if the website has a page at `404.html` for some reason.
3. Download any extra urls specified in `extra-urls.txt`.

The download is followed by three post-processing steps:

1. Remove all query parameters (only `?ver`) from the downloaded files using `.github/bin/cleanup-querystrings.py`.
2. Use `sed` to replace the website's URL with the GitHub Pages url in all files.
3. Minify all HTML files using [minify](https://github.com/tdewolff/minify).

After these steps, the files are deployed to GitHub Pages: [ftcunion.github.io](https://ftcunion.github.io).

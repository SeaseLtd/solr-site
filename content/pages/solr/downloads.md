Title: Downloads
URL: solr/
save_as: solr/downloads.html
template: solr/page

# Solr Downloads

Official releases are usually created when the [developers](../whoweare.html) feel there are
sufficient changes, improvements and bug fixes to warrant a release.  Due to the voluntary
nature of Solr, no releases are scheduled in advance.

## Solr 8.3.0 ##

Solr 8.3.0 is the most recent Apache Solr release.

 - Source release: [solr-8.3.0-src.tgz](https://www.apache.org/dyn/closer.lua/lucene/solr/8.3.0/solr-8.3.0-src.tgz) [[PGP](https://www.apache.org/dist/lucene/solr/8.3.0/solr-8.3.0-src.tgz.asc)] [[SHA512](https://www.apache.org/dist/lucene/solr/8.3.0/solr-8.3.0-src.tgz.sha512)]
 - Binary releases:  [solr-8.3.0.tgz](https://www.apache.org/dyn/closer.lua/lucene/solr/8.3.0/solr-8.3.0.tgz) [[PGP](https://www.apache.org/dist/lucene/solr/8.3.0/solr-8.3.0.tgz.asc)] [[SHA512](https://www.apache.org/dist/lucene/solr/8.3.0/solr-8.3.0.tgz.sha512)] / [solr-8.3.0.zip](https://www.apache.org/dyn/closer.lua/lucene/solr/8.3.0/solr-8.3.0.zip) [[PGP](https://www.apache.org/dist/lucene/solr/8.3.0/solr-8.3.0.zip.asc)] [[SHA512](https://www.apache.org/dist/lucene/solr/8.3.0/solr-8.3.0.zip.sha512)]
 - [Change log](https://lucene.apache.org/solr/8.3.0/changes/Changes.html)

## Solr 7.7.2 ##

Solr 7.7.2 is the last release in the 7.x series.

 - Source release: [solr-7.7.2-src.tgz](https://www.apache.org/dyn/closer.lua/lucene/solr/7.7.2/solr-7.7.2-src.tgz) [[PGP](https://www.apache.org/dist/lucene/solr/7.7.2/solr-7.7.2-src.tgz.asc)] [[SHA512](https://www.apache.org/dist/lucene/solr/7.7.2/solr-7.7.2-src.tgz.sha512)]
 - Binary releases:  [solr-7.7.2.tgz](https://www.apache.org/dyn/closer.lua/lucene/solr/7.7.2/solr-7.7.2.tgz) [[PGP](https://www.apache.org/dist/lucene/solr/7.7.2/solr-7.7.2.tgz.asc)] [[SHA512](https://www.apache.org/dist/lucene/solr/7.7.2/solr-7.7.2.tgz.sha512)] / [solr-7.7.2.zip](https://www.apache.org/dyn/closer.lua/lucene/solr/7.7.2/solr-7.7.2.zip) [[PGP](https://www.apache.org/dist/lucene/solr/7.7.2/solr-7.7.2.zip.asc)] [[SHA512](https://www.apache.org/dist/lucene/solr/7.7.2/solr-7.7.2.zip.sha512)]
 - [Change log](https://lucene.apache.org/solr/7_7_2/changes/Changes.html)

## Solr Reference Guide

[Download the official docuentation](https://lucene.apache.org/solr/guide/)

## Past versions ##

Archives for all past versions of Solr are available at
[the Apache archives](https://archive.apache.org/dist/lucene/solr/).

## About downloads ##

### Verify downloads ###

The above release files should be verified using the PGP signatures and the
[project release KEYS](https://www.apache.org/dist/lucene/KEYS). See
[verification instructions](https://www.apache.org/dyn/closer.cgi#verify) for a
description of using the PGP and KEYS files for verification. SHA checksums
are also provided as alternative verification method.

### File names ###

The `solr-VERSION.zip` or `solr-VERSION.tgz` files (where `VERSION` is the version number of
the release, e.g. `8.1.1`) contain Apache Solr, html documentation and a tutorial.

The `solr-VERSION-src.tgz` file contains the full source code for that version.

### About versions and support ###

Apache Solr is under active development with frequent feature releases on the current major version.
The **previous** major version may still receive security- and bug fixes as point releases, thus taking the role
of the LTS (Long Term Support) version.
Older versions are considered EOL (End Of Life) and will not be further
updated. For this reason it may also be difficult to obtain community support for EOL versions.

Large changes or changes that break compatibility with existing
functionality are normally only included in the **next** major version.

<table>
<tr align=left><th>Version</th><th>Description</th></tr>
<tr align=left><td>8.x</td><td>Current major version for feature releases (STABLE)</td></tr>
<tr align=left><td>7.7.x</td><td>Version in the previous major release for bugfixes only (LTS)</td></tr>
<tr align=left><td>9.0</td><td>Next major version, yet to be released (UNSTABLE)</td></tr>
<tr align=left><td><7.7</td><td>All older versions are End Of Life (EOL)</td></tr>
</table>

For more about versions and upgrading Solr, see the
[Reference Guide chapter “Upgrade Notes”](https://lucene.apache.org/solr/guide/solr-upgrade-notes.html) and ["System Requirements"](https://lucene.apache.org/solr/guide/solr-system-requirements.html).
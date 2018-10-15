# Downloading all Wikipedia history
Purely downloading; no reprocessing is happening here.

## Requirements
- `/data`: 150GB of free space

## Arguments
- `revision`: the date of the download. You can use `latest` or use any
  subdirectory of
  [https://dumps.wikimedia.org/enwiki/](https://dumps.wikimedia.org/enwiki/).

## Outputs
- `/data/wikipedia-history-$revision`
- `/data/wikipedia-history-$revision.torrent`

## Download details
History files are provided in multiple formats; I'm going to use 7zip here
because those files are _much_ smaller -- like 1/10th of the bzip2's. This makes
sense given 7z's long lookback window.

```sh
$ ni https://dumps.wikimedia.org/enwiki/latest/ \
     p'/href="([^"]+\.7z)"/g' \
     p'"https://dumps.wikimedia.org/enwiki/latest/$_"' \
  | xargs wget -c
```

Now we can use ni's 7z accessors to read the stream; for example:

```sh
$ ni 7z://enwiki-latest-pages-meta-history1.xml-p10p2101.7z \<r10
<mediawiki xmlns="http://www.mediawiki.org/xml/export-0.10/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.mediawiki.org/xml/export-0.10/ http://www.mediawiki.org/xml/export-0.10.xsd" version="0.10" xml:lang="en">
  <siteinfo>
    <sitename>Wikipedia</sitename>
    <dbname>enwiki</dbname>
    <base>https://en.wikipedia.org/wiki/Main_Page</base>
    <generator>MediaWiki 1.32.0-wmf.19</generator>
    <case>first-letter</case>
    <namespaces>
      <namespace key="-2" case="first-letter">Media</namespace>
      <namespace key="-1" case="first-letter">Special</namespace>
```

We end up with a series of `<page>` elements, each with revisions:

```sh
$ ni . p'"7z://$_"' \<\<rp'/<page/../<\/page>/'
  <page>
    <title>AccessibleComputing</title>
    <ns>0</ns>
    <id>10</id>
    <redirect title="Computer accessibility" />
    <revision>
      <id>233192</id>
      <timestamp>2001-01-21T02:12:21Z</timestamp>
      <contributor>
        <username>RoseParks</username>
        <id>99</id>
      </contributor>
      <comment>*</comment>
      <model>wikitext</model>
      <format>text/x-wiki</format>
      <text xml:space="preserve">This subject covers

* AssistiveTechnology

* AccessibleSoftware

* AccessibleWeb

* LegalIssuesInAccessibleComputing

</text>
      <sha1>8kul9tlwjm9oxgvqzbwuegt9b2830vw</sha1>
    </revision>
    <revision>
      <id>862220</id>
      <parentid>233192</parentid>
      <timestamp>2002-02-25T15:43:11Z</timestamp>
      <contributor>
        <username>Conversion script</username>
        <id>0</id>
      </contributor>
      <minor />
      <comment>Automated conversion</comment>
      <model>wikitext</model>
      <format>text/x-wiki</format>
      <text xml:space="preserve">#REDIRECT [[Accessible Computing]]
</text>
      <sha1>i8pwco22fwt12yp12x29wc065ded2bh</sha1>
    </revision>
...
```

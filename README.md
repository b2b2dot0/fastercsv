[![Build Status](https://travis-ci.org/b2b2dot0/fastercsv.png)](https://travis-ci.org/b2b2dot0/fastercsv)

# Read Me

by James Edward Gray II

## Description

Welcome to FasterCSV.

FasterCSV is intended as a replacement to Ruby's standard CSV library.  It was designed to address concerns users of that library had and it has three primary goals:

1.  Be significantly faster than CSV while remaining a pure Ruby library.
2.  Use a smaller and easier to maintain code base.  (FasterCSV is larger now, 
    but considerably richer in features.  The parsing core remains quite small.)
3.  Improve on the CSV interface.

Obviously, the last one is subjective.  If you love CSV's interface, odds are
good this one won't suit you.  I did try to defer to that interface whenever I
didn't have a compelling reason to change it though, so hopefully this won't be
too radically different.

## What's Different From CSV?

I'm sure I'll miss something, but I'll try to mention most of the major differences I am aware of, to help others quickly get up to speed:

### CSV Parsing

* FasterCSV has a stricter parser and will throw MalformedCSVErrors on
  problematic data.
* FasterCSV has a less liberal idea of a line ending than CSV.  What you set as
  the <tt>:row_sep</tt> is law.
* CSV returns empty lines as <tt>[nil]</tt>.  FasterCSV calls them <tt>[]</tt>.
* FasterCSV has a much faster parser.

### Interface

* FasterCSV uses Hash-style parameters to set options.
* FasterCSV does not have generate_row() or parse_row() from CSV.
* FasterCSV does not have CSV's Reader and Writer classes.
* FasterCSV::open() is more like Ruby's open() than CSV::open().
* FasterCSV objects support most standard IO methods.
* FasterCSV has a new() method used to wrap objects like String and IO for
  reading and writing.
* FasterCSV::generate() is different from CSV::generate().
* FasterCSV does not support partial reads.  It works line-by-line.
* FasterCSV does not allow the instance methods to override the separators for
  performance reasons.  They must be set in the constructor.

If you use this library and find yourself missing any functionality I have trimmed, please {let me know}[mailto:james@grayproductions.net].

## Documentation

See FasterCSV for documentation.

## Installing

See the INSTALL file for instructions.

## What is CSV, really?

FasterCSV maintains a pretty strict definition of CSV taken directly from {the RFC}[http://www.ietf.org/rfc/rfc4180.txt].  I relax the rules in only one place and that is to make using this library easier.  FasterCSV will parse all valid CSV.

What you don't want to do is feed FasterCSV invalid CSV.  Because of the way the CSV format works, it's common for a parser to need to read until the end of the file to be sure a field is invalid.  This eats a lot of time and memory.

Luckily, when working with invalid CSV, Ruby's built-in methods will almost always be superior in every way.  For example, parsing non-quoted fields is as easy as:

  data.split(",")

## Questions and/or Comments

Feel free to email {James Edward Gray II}[mailto:james@grayproductions.net] with
any questions.

# Filters

You can filter commits in git.

## By Date

`--before` is used to filter commits before a certain date
```
git log --before=[date]
```
`--after` is used to get commits after a certain date
```
git log --after=[date]
```
> Date should be in YYYY-MM-DD format

## By Author

Using `--author` filters the commit log with commits done by the given author

```
git log --author="author_name"
```

## By File

You can also find commits which deals with a particular file

```
git log -- [filename]
```

## By Commit Message

You can filter the commit log with commit msgs containg any specific keyword _or_ the complete message

```
git log --grep="commit msg"
```
---

> Multiple filters can also be combined

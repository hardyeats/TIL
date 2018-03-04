>  warning: LF will be replaced by CRLF in some-title.md.
>
>  The file will have its original line endings in your working directory.

In Unix systems the end of a line is represented with a line feed (LF). In windows a line is represented with a carriage return (CR) and a line feed (LF) thus (CRLF). when you get code from git that was uploaded from a unix system they will only have an LF.

If you want to turn this warning off, type this in the git command line

```bash
git config core.autocrlf true
```

If you want to make an intelligent decision how git should handle this, [read the documentation](http://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration#Formatting-and-Whitespace)
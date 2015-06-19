---
excerpt: Deploying to an Amazon S3 bucket
---

Deploying to an Amazon S3 bucket
================================


So, I currently have a public folder, reachable at http://s3.amazonaws.com/_PublicFolderName_.  (I wonder if I should
change the name of that folder to something that's not my name?)

The folder isn't browsable, but stuff in it is publicly viewable, so it's just a matter of uploading to the folder and
linking to the right URL.

Uploading
---------

The AWS console has an "Upload" function, but is there a command-line tool I can use?

Why, _yes_, there does indeed appear to be!
[http://docs.aws.amazon.com/powershell/latest/userguide/pstools-welcome.html](http://docs.aws.amazon.com/powershell/latest/userguide/pstools-welcome.html)

(More later, I hope.)

...

Ok, now it's later, but I can't figure this out using the PowerShell tools.  I'll have to try again later, from my Linux
machine.  Tools are available here: [https://aws.amazon.com/cli/](https://aws.amazon.com/cli/).

-----

Ok, now it's a whole day later, but I've figured it out.

Install the AWS Linux tools.

`aws config`

Enter your data.  You can use an Amazon IAM user.  I'd select output format of "text" (default is "json").

(IAM is Identity and Access Management).

After that, `cd` to your source directory and knock yourself out:

    for f in gradient-data.js gradient-editor.html gradient-editor.css; do
      aws s3 cp $f s3://JohnLuskPublic/GradientEditorWeb/$f
    done


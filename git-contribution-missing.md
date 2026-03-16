# Fixing GitHub Contributions Not Appearing (Email Mismatch)

## Problem

Sometimes you push commits to GitHub but the contribution graph does not show a green square for that day. The repository updates correctly, but the activity is missing from your GitHub profile.

This usually happens because the email used in the Git commit does not match the email associated with your GitHub account.

For example, a commit might appear as:

```
Author: tanmoy <tanmoy@MacBookUltraProMax.local>
```

Even though the commit was pushed successfully, GitHub cannot associate this email with the account, so it does not count toward the contribution graph.

---

## Why This Happens

When Git is installed on a new machine, it often automatically configures the email using the computer's local hostname. This results in an email format such as:

```
username@computer-name.local
```

For example:

```
tanmoy@MacBookUltraProMax.local
```

Since this email is not registered in your GitHub account, GitHub cannot link the commit to your profile.

---

## Using GitHub's Noreply Email

GitHub provides a private email that allows commits to be associated with your account without exposing your real email address.

The format is:

```
<github-user-id>+<username>@users.noreply.github.com
```

Example:

```
123456+tanmoy456@users.noreply.github.com
```

Find the "github-user-id" in github > settings >> Emails >> Keep my email addresses private


This email keeps your personal email private while ensuring that commits are counted in your contribution graph.

---

## Configure Git Correctly

To fix the issue, configure Git with your GitHub username and noreply email.

Run the following commands in your terminal:

```
git config --global user.name "tanmoy456"
git config --global user.email "123456+tanmoy456@users.noreply.github.com"
```

After running these commands, all future commits will use the correct author information.

---

## Verify Your Configuration

You can verify your Git configuration with:

```
git config --global --list
```

Expected output:

```
user.name=tanmoy456
user.email=123456+tanmoy456@users.noreply.github.com
```

---

## Checking the Author Before Pushing

Before pushing a commit, you can confirm the author information with:

```
git log -1
```

You should see something like:

```
Author: tanmoy456 <123456+tanmoy456@users.noreply.github.com>
```

If the email matches your GitHub noreply email, the commit will be counted in your GitHub contributions.

---

## Fixing an Existing Commit

If you already made a commit using the wrong email, you can update the author information by amending the commit.

```
git commit --amend --author="tanmoy456 <123456+tanmoy456@users.noreply.github.com>"
git push --force
```

This rewrites the commit with the correct email so that GitHub can associate it with your account.

---

## Useful Debug Commands

Check the email currently used by Git:

```
git config user.email
```

Check the author of the most recent commit:

```
git log -1
```

Show all Git configuration settings:

```
git config --list
```

---

## Summary

The GitHub contribution graph depends on the email stored in the commit metadata. If the commit email does not match one registered in your GitHub account, the contribution will not appear on your profile.

By configuring Git with your GitHub noreply email, you can ensure that all future commits are correctly attributed to your account while keeping your personal email private.


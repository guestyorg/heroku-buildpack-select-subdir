# Heroku Buildpack Select Subdir - with CD

Allows you to have a monolithic repo with multiple Heroku apps in different subdirectories (like Google!).

Unlike https://github.com/Pagedraw/heroku-buildpack-select-subdir, this buildpack will add the `cd <subdir>` bit
into the Procfile when copying it, which lets you use the same Procfile you would use if you were using a repo
per subdirectory.

## Usage

* Write a bunch of Procfiles and scatter them throughout your code base.
* Create a bunch of Heroku apps.
* For each app do `heroku buildpacks:set -a <app> https://github.com/Pagedraw/heroku-buildpack-select-subdir`
* For each app, specify a `<subdir>` and a buildpack by setting
```heroku config:add BUILDPACK='<subdir>=https://github.com/desired/heroku-buildpack' -a <app>```
* For each app, `git push git@heroku.com:<app> master`

This buildpack assumes each subdirectory added above has a Procfile in it. It will

1. Run each app's specified buildpack at the corresponding subdirectory
2. Copy the Procfile found at the specified subdirectory to the root
3. Change each process definition so it `cd`s into the subdirectory before running.
4. Source all files added to the `.profile.d/` directory by the buildpack from 1.

## License

MIT

This is a variant of:
   <https://github.com/actions/upload-release-asset>

Instead of just cloning it, I opted to first write a template and then 
to add the scripts into it. This way, I was able to understand a little
better about how to work with npm.

The template was created with:

```
npm install @actions/core @actions/exec @actions/github
npm install --save-dev @vercel/ncc jest eslint
```

And the actual `dist/` content from:

```
npm run build && git add dist/
```

As a plus, such procedure allowed me to to double-check if everything
is OK there, as checking the contents of the executables under dist/
is hard, as it is produced via `npm build`.

Assuming that the code inside @actions/* are verified by Github,
and that the development tools from npm, the contents of dist/ should
also be OK. So, from security point of view, all that I needed to
check were to verify the content of the scripts under `src/`.

Right now, the unit tests inside `tests/` aren't working, but those
didn't pass either when used at the original repo. A fix for it
is welcomed. I'm not a Javascript programmer ;-)

This variant should have just one new feature: it should allow adding
a workflow_dispatch to the workflow action callers, like:

```
on:
  release:
    types:
      - created
      - published

  workflow_dispatch:
    inputs:
      release:
        description: 'release ID for uploading binaries'
        required: false
```

And let the script to run even after a release.

PS.: I don't have any big expectations here, except to help
me to work with my own repositories ;-)

Feel free to send me patches that won't break my work,
but I won't be able to work much on it. So, don't expect
much activities on this project.

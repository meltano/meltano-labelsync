## Production Documentation

The full YAML spec is defined in the [LabelSync product documentation](https://www.notion.so/YAML-917804788a604e099b03361edb4f628d).

### Defining Repositories

All repositories currently enrolled in label syncing are defined under the `repos` key.

The `*` repository is a special one which captures any newly created repositories. 

To enroll a new repository, add a new key under `repos` with the following information:

```yaml
  <repo-name>:
    config:
      removeUnconfiguredLabels: true
    labels:
      <<: *all_labels
```

`removeUnconfiguredLabels` means that any new labels created in the Project will be deleted once LabelSync runs.

The labels key is using a merge reference meaning it will use all of the values defined at the alias `all_labels`. 

This is a convenient way to organize groups of labels and use them in multiple places.

### Defining Labels

The following is a representative example of how to define an update a label:

```yaml
  "Accepting Pull Requests":
    color: *green
    description: "Relevant description"
    alias:
      - "accepting pull requests"
      - "accepting merge requests"
      - "Accepting Merge Requests"
```

This definition indicates the following:

* A label called `Accepting Pull Requests` should exist
* It should be colored "green"
  * This is referencing a YAML anchor which is defined as follows:

  ```yaml
  colors:
      green: &green "#0E8A16"
  ```
* It has as description
* It has several aliases

Aliases are how we can rename labels and re-label existing issues. 
In the above example any issue that has one of the alias labels will get the correct `Accepting Pull Requests` label assigned to it. 

It is recommended to always leave the aliases list in case new repositories are enrolled into LabelSync.

### PRs

Assign any PR to @tayloramurphy for review.

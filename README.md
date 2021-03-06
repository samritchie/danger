# Danger :no_entry_sign:

[![License](http://img.shields.io/badge/license-MIT-green.svg?style=flat)](https://github.com/orta/danger/blob/master/LICENSE)
[![Gem](https://img.shields.io/gem/v/danger.svg?style=flat)](http://rubygems.org/gems/danger)

Formalize your Pull Request etiquette.

*Note:* Not ready for public usage yet. Work in progress

-------
<p align="center">
    <a href="#installation">Installation</a> &bull; 
    <a href="#usage">Usage</a> &bull; 
    <a href="#dsl">DSL</a> &bull; 
    <a href="#constraints">Constraints</a> &bull; 
    <a href="#development">Development</a> &bull; 
    <a href="#contributing">Contributing</a>
</p>

-------

## Installation

Add this line to your application's [Gemfile](https://guides.cocoapods.org/using/a-gemfile.html):

```ruby
gem 'danger'
```

## Usage

In CI run `bundle exec danger`.  This will look at your `Dangerfile` and provide some feedback based on that.

## DSL

&nbsp;  | &nbsp; | Danger :no_entry_sign:
-------------: | ------------- | ----
:sparkles: | `lines_of_code` | The total amount of lines of code in the diff
:monorail: | `files_modified` |  The list of files modified
:ship: | `files_added` | The list of files added
:pencil2: | `files_removed` | The list of files removed
:wrench: | `pr_title` | The title of the PR
:thought_balloon: | `pr_body` | The body of the PR



You can access more detailed information  by looking through:

&nbsp;  | &nbsp; | Danger :no_entry_sign:
-------------: | ------------- | ----
| :sparkles: |  `env.travis` | Details on the [Travis CI](https://travis-ci.org) integration
| :tophat: | `env.circle` | Details on the [Circle CI](https://circleci.com) integration
| :cloud: | `env.buildkite` | Details on the [Buildkite](https://buildkite.com) integration
| :octocat: | `env.github.pr_json` | The full JSON for the pull request
| :ghost: | `env.git.diff` | The full [GitDiff](https://github.com/schacon/ruby-git/blob/master/lib/git/diff.rb) file for the diff.

You can then create a `Dangerfile` like the following:

``` ruby
# Easy checks
warn("PR is classed as Work in Progress") if pr_title.include? "[WIP]"

if lines_of_code > 50 && files_modified.include? "CHANGELOG.yml" == false
  fail("No CHANGELOG changes made")
end

# Stop skipping some manual testing
if lines_of_code > 50 && pr_title.include? "📱" == false
   fail("Needs testing on a Phone if change is non-trivial")
end
```

## Constraints

* **GitHub** - Built with same-repo PRs in mind
* **Git** - Built with master as the merge branch

## Special Thanks

Thanks [@orta](https://twitter.com/orta) for starting this project and handing it over to the `fastlane` organisation

## License

> This project and all fastlane tools are in no way affiliated with Apple Inc. This project is open source under the MIT license, which means you have full access to the source code and can modify it to fit your own needs. All fastlane tools run on your own computer or server, so your credentials or other sensitive information will never leave your own computer. You are responsible for how you use fastlane tools.

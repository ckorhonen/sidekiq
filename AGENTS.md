# Repository guide

## Map and setup

`lib/sidekiq/` contains job processing, client/server middleware, and APIs; `web/` contains the dashboard; `test/` contains Minitest coverage. `myapp/`, `bare/`, and `examples/` are integration/demo surfaces. Preserve the license distinctions in `LICENSE.txt` and `COMM-LICENSE.txt`.

The gem requires Ruby 3.2+. README lists Redis 7+, Valkey 7.2+, or Dragonfly 1.27+; the Gemfile defaults to Rails 8, so match a supported Ruby/Rails pair rather than assuming every minimum combines. CI exercises Ruby 3.2/4.0 and Rails 7.1/8.1. Install with `bundle install`, setting `RAILS_VERSION` consistently with the target combination when needed.

## Verification and actions

`bundle exec rake` runs Standard, ERB lint, and tests; `bundle exec rake test` runs Minitest; `bundle exec rake lint:herb` checks web templates. Focus a Rake test with `TEST=test/client_test.rb` when appropriate. **Tests call `flushdb` through `test/helper.rb` and default to localhost Redis database 0.** Set `REDIS_URL` to a verified disposable test instance before running them; never point tests at shared queues. Web changes also need an inspected browser flow. CI filters the `main` branch, while this fork's default branch is `master`; do not assume a fork PR will trigger it.

Start with `git status --short`, preserve unrelated work, and complete authorized local changes through relevant checks and repair. Routine reversible choices do not need extra approval. Starting production workers, draining queues, load testing, changing shared Redis, or publishing gems requires explicit authorization. If the isolated database or compatible toolchain is unavailable, name that prerequisite and continue independent checks. For prose-only edits, verify sources and run `git diff --check`; close with changed paths, actual checks/results, and remaining runtime gaps.

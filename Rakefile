require 'puppetlabs_spec_helper/rake_tasks'
require 'metadata-json-lint/rake_task'
require 'rubocop/rake_task'

RuboCop::RakeTask.new

task :librarian_spec_prep do
  sh 'librarian-puppet install --path=spec/fixtures/modules/'
end
task :spec_prep => :librarian_spec_prep

# Override puppetlabs_spec_helper's default lint settings
# * Don't want to ignore so many tests
# * Don't want to run lint on upstream modules
Rake::Task[:lint].clear
PuppetLint::RakeTask.new(:lint) do |config|
  config.fail_on_warnings = true
  config.ignore_paths = [
    'modules/**/*.pp',
    'pkg/**/*.pp',
    'spec/**/*.pp',
    'vendor/**/*.pp',
  ]
end

desc 'Run syntax, lint, metadata and spec tests.'
task :test => [
  :syntax,
  :lint,
  :metadata_lint,
  :spec,
  :rubocop,
]

require 'rubygems'
require 'rubygems/package_task'
require 'rake/extensiontask'
require 'pp'

task :default => [:compile]

spec = eval(File.read('opcua-server.gemspec'))
Rake::ExtensionTask.new "opcua/server", spec

Gem::PackageTask.new(spec) do |pkg|
  pkg.need_zip = true
  pkg.need_tar = true
  # `rm pkg/* -rf`
  # `ln -sf #{pkg.name}.gem #{pkg.package_dir}/#{spec.name}.gem`
end

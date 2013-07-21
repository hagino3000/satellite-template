# vim: et sts=2 ts=2 sw=2 ft=ruby:
task 'default' => 'generate_config'

task 'generate_config' do
  configs = FileList.new 'config.yml', 'config/*.yml'
  File.open '_config.yml', 'w' do |config_file|
    configs.each do |config|
      file = File.open config do |f|
        config_file << "### #{config} ###\n"
        config_file << f.read
      end
    end
  end
end


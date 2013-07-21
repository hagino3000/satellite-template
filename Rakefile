# vim: et sts=2 ts=2 sw=2 ft=ruby:

TEMPLATE_FILES = [
  'browser.html',
  'bubbletree-map.html',
  'dailybread.html',
  'dailybread_white.html',
]

task 'default' => ['generate_config', 'generate_template']

task 'generate_config' do
  configs = FileList.new 'common.yml', 'config/*.yml'
  File.open '_config.yml', 'w' do |config_file|
    configs.each do |config|
      file = File.open config do |f|
        config_file << "### #{config} ###\n"
        config_file << f.read
      end
    end
  end
end

task 'generate_template' do
  regions = (FileList.new 'config/*.yml').map do |path|
    path.sub %r!^config/(.*)\.yml$!, '\1'
  end
  regions.each do |region|
    unless Dir.exist? region then
      mkdir region
    end
    TEMPLATE_FILES.each do |file|
      cp file, region
    end
  end
end


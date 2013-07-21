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
      unless File.exist? File.join([region, file]) then
        cp file, region
      end
    end
    images = FileList.new 'img', 'img/*', 'img/*/*'
    images.each do |image|
      path = File.join [region, image]
      unless (File.basename image).include? '.' then
        unless Dir.exist? path then
          mkdir path
        end
      else
        unless File.exist? path then
          cp image, path
        end
      end
    end
  end
end


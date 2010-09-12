desc "Update the ports index"
task :portindex do
  chdir "ports" do
    sh "portindex"
  end
end

desc "Install this tree into the macports sources configuration"
task :install do
  uri = "file://#{File.expand_path('../ports', __FILE__)}"
  srccnf = '/opt/local/etc/macports/sources.conf'
  exists = open(srccnf) do |f|
    f.grep(Regexp.new(Regexp.escape(uri))).any?
  end
  if exists
    puts "#{uri} source already exists"
  else
    open(srccnf, 'r+') do |f|
      old = f.read
      f.rewind
      f.puts "#{uri} [nosync]"
      f.puts old
    end
    puts "#{uri} source written"
  end
end

task :default => :portindex
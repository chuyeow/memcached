require 'rubygems'
require 'rake'

begin
  require 'jeweler'
  Jeweler::Tasks.new do |gem|
    gem.name = "chuyeow-memcached"
    gem.summary = %Q{Fork of the interface to the libmemcached C client - adds experimental support for items bigger than the 1MB memcached limit.}
    gem.description = %Q{Fork of the interface to the libmemcached C client - adds experimental support for items bigger than the 1MB memcached limit.}
    gem.email = "chuyeow@gmail.com"
    gem.homepage = "http://github.com/chuyeow/memcached"
    gem.authors = ["Cheah Chu Yeow"]
  end
  Jeweler::GemcutterTasks.new
rescue LoadError
  puts "Jeweler (or a dependency) not available. Install it with: gem install jeweler"
end

task :exceptions do
  $LOAD_PATH << "lib"
  require 'memcached'
  Memcached.constants.sort.each do |const_name|
    const = Memcached.send(:const_get, const_name)
    next if const == Memcached::Success or const == Memcached::Stored
    if const.is_a? Class and const < Memcached::Error
      puts "* Memcached::#{const_name}"
    end
  end
end

task :valgrind do
  exec("valgrind  --tool=memcheck --leak-check=yes --show-reachable=no --num-callers=15 --track-fds=yes ruby #{File.dirname(__FILE__)}/test/profile/valgrind.rb")
end

task :profile do
 exec("ruby #{File.dirname(__FILE__)}/test/profile/profile.rb")
end

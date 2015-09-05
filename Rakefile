require 'json'
$LOAD_PATH << File.join(File.dirname(__FILE__))
require 'rake'

desc "Build virtualbox Vagrant box via packer"
task :build do |task|
  puts "running rake task: #{task.name}"
  version = get_box_version
  puts "box version: #{version}"
  cmd = "packer-io build -only=virtualbox-iso -var 'box_version=#{version}' arch-template.json"
  system_or_die(cmd, "ERROR running packer")
end

def get_box_version
  mydir = File.dirname( __FILE__)
  version = `git --git-dir=#{mydir}/.git --work-tree=#{mydir} rev-parse --short HEAD`
  version = version.strip
  version = 'none' if version == ''
  dirty = false
  res = system("git --git-dir=#{mydir}/.git --work-tree=#{mydir} diff --no-ext-diff --quiet --exit-code")
  if ! res
    dirty = true
  end
  res = system("git --git-dir=#{mydir}/.git --work-tree=#{mydir} diff-index --cached --quiet HEAD --")
  if ! res
    dirty = true
  end
  if dirty
    version = "#{version}-dirty"
    # die if dirty
    puts "ERROR: git repository is dirty; please commit before building!"
    exit!(1)
  end
  return version
end

def system_or_die(cmd, fail_msg=nil)
  puts "running: '#{cmd}'"
  res = system(cmd)
  if ! res
    if fail_msg.nil?
      $stderr.puts "ERROR running command: #{cmd}"
    else
      $stderr.puts fail_msg
    end
    exit!(1)
  end
end

def system_puts(cmd)
  puts "running: '#{cmd}'"
  res = system(cmd)
end

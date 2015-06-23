def start_chef_zero
  @zero_pid = spawn('chef-zero')
  Process.detach(@zero_pid)
  @zero_pid
end

def stop_chef_zero
  Process.kill('HUP', @zero_pid)
end

def berks_install
  system('berks install && berks upload')
end

desc 'Build AWS Server Marketplace Images'
task :publish_aws_server do
  start_chef_zero
  berks_install
  system("chef-client -c .chef/client.rb -o 'marketplace_image::aws_server_publisher'")
  stop_chef_zero
end

desc 'Build AWS Analytics Marketplace Images'
task :publish_aws_analytics do
  start_chef_zero
  berks_install
  system("chef-client -c .chef/client.rb -o 'marketplace_image::aws_analytics_publisher'")
  stop_chef_zero
end

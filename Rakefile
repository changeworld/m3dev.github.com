require 'yaml'
TALKS_FILE_PATH = 'data/talks.yml'.freeze
QUESTIONS = { 'title' => 'Title',
              'by' => 'Created by',
              'github_id' => 'Your GitHub id',
              'source' => 'embed tag' }.freeze

desc 'Add Tech Talk slide'
task :add_slide do
  yml = YAML.load_file(TALKS_FILE_PATH)

  new = {}
  QUESTIONS.each do |key, msg|
    print "#{msg} >"
    tmp = STDIN.gets.chomp
    tmp = msg.split(',')[tmp.to_i - 1].split(':')[1].gsub(/\s/, '') rescue tmp if tmp.to_i >= 1
    new[key] = tmp
  end

  #変更した変更を書き出す
  open(TALKS_FILE_PATH, 'w') do |f|
    YAML.dump(yml.insert(0, new), f)
  end

  # Create new branch
  head_name = $1 if Socket.gethostname =~ /^(m3\-20[\d]+)mac/
  branch_name = "feature/#{head_name}_#{Time.now.strftime('%Y%m%d%H%M%s')}"
  system("git checkout -b #{branch_name}")
  system("git add #{TALKS_FILE_PATH}")
  system("git commit -m 'add slide title: #{new['title']}'")
end
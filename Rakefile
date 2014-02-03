require 'date'
require 'logger'
require 'os'

desc "Clear Screenshot dir"
task :clear_screenshots do
  screenshot_path = `defaults read com.apple.screencapture location`
  screenshot_path.delete!("\n")

  if screenshot_path == "" || !File.directory?(screenshot_path)

    log "remove_screenshots.log", Logger::ERROR, "No custom Screenshot DIR. I will not remove files from the desctop."
    exit -1
  end

  files_in_dir = Dir.entries(screenshot_path)
  files_in_dir.each do |f|
    f_path = screenshot_path + "/" + f
    days_ago = (Date.today - 30).to_time
    if File.ftype(f_path) == "file"
      if File.mtime(f_path) < days_ago
        begin
          File.delete f_path
          log "remove_screenshots.log", Logger::INFO, "rm " + f_path
        rescue Exception => e
          log "remove_screenshots.log", Logger::ERROR, "Can't remove #{f_path}: #{e.message}"
        end

      end
    end
  end
end




def log(file, level, message)
  dir = "custom_rake"
  if OS.mac?
    logging_dir = ENV['HOME'] + "/Library/Logs/" + dir
  else
    #todo
    exit -1
  end

  unless File.directory?(logging_dir)
    Dir.mkdir(logging_dir)  
  end

  log = Logger.new( logging_dir + "/" + file, 'monthly' )
  log.add level, message
end

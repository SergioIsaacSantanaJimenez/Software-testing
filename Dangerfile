# Verify that commit titles have a maximum of 50 characters
git.commits.each do |commit|
  message_lines = commit.message.split("\n")
  title = message_lines.first
  
  if title.length > 50
    fail "Commit #{commit.sha} title has #{title.length} characters, but should have a maximum of 50."
  end
  
  # Verify that there's an empty line between the title and description
  if message_lines.count > 1
    if message_lines[1] && !message_lines[1].empty?
      fail "There should be an empty line between the title and description in commit #{commit.sha}."
    end
    
    # Verify that the description has at least 5 characters
    description = message_lines[2..-1].join("\n").strip
    if !description.empty? && description.length < 5
      fail "Commit #{commit.sha} description has #{description.length} characters, but should have at least 5."
    end
    
    # Verify that each line in the description doesn't have more than 72 characters
    message_lines[2..-1].each_with_index do |line, index|
      if line.length > 72
        fail "Line #{index + 3} of commit #{commit.sha} description has #{line.length} characters, but should have a maximum of 72."
      end
    end
  end
end

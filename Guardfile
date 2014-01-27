guard :shell, :all_on_start => true do
  watch("lua-for-rubyists.md") { regen }
  watch("css/style.css")       { regen }
end

def regen
  system('rm -rf lua-for-rubyists')
  system('mdpress -i images lua-for-rubyists.md')
  system('rm -rf lua-for-rubyists/css')
  system('cp -r css lua-for-rubyists')
end

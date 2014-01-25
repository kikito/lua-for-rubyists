guard :shell do
  watch 'lua-for-rubyists.md' do
    system('rm -rf lua-for-rubyists')
    system('mdpress -i images lua-for-rubyists.md')
    system('rm -rf lua-for-rubyists/css')
    system('cp -r css lua-for-rubyists')
  end
end

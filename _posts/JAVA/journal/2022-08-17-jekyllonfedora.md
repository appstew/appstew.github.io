---
layout: post
title: 220817 페도라에 개발 환경 세팅 일지
category: JAVA
tags: journal
---

- [220817 충돌없는 3멀티부트 페도라 구성 일지](2022-08-17-220817.md) 글에 이어서, 개발환경 세팅 기록

# 1.jekyll 및 github blog 환경 세팅

- jekyll 을 설치하다보면 페도라에서 하나씩 의존 패키지를 찾아 ruby gem 과 gem 등 다 설치하게 되겠지만 그래도 혹시 주의사항이 있을지 모르니 공식 사이트의 안내문서도 참고하자.

- https://jekyllrb.com/
- https://rubygems.org/pages/download
- https://www.ruby-lang.org/ko/documentation/installation/
- https://rubyonrails.org/ 
- https://namu.wiki/w/Ruby%20on%20Rails ruby on rails 란?
- 
- 관심이 생긴 사이트
- https://try.ruby-lang.org


1. gem install bundler jekyll

```bash
[dami@fedora install]$ ls
[dami@fedora install]$ ls -alh
total 8.0K
drwxr-xr-x. 2 dami dami 4.0K Aug 17 19:07 .
drwxr-xr-x. 4 dami dami 4.0K Aug 17 19:07 ..
[dami@fedora install]$ gem install bundler jekyll
bash: gem: command not found...
Install package 'rubygems' to provide command 'gem'? [N/y] y
```
```bash
* Waiting in queue... 
 * Waiting for authentication... 
 * Waiting in queue... 
 * Downloading packages... 
 * Requesting data... 
 * Testing changes... 
 * Installing packages... 
Fetching bundler-2.3.20.gem
Successfully installed bundler-2.3.20
Parsing documentation for bundler-2.3.20
Installing ri documentation for bundler-2.3.20
Done installing documentation for bundler after 0 seconds
Fetching unicode-display_width-1.8.0.gem
Fetching rouge-3.30.0.gem
Fetching mercenary-0.4.0.gem
Fetching forwardable-extended-2.6.0.gem
Fetching pathutil-0.16.2.gem
Fetching liquid-4.0.3.gem
Fetching terminal-table-2.0.0.gem
Fetching safe_yaml-1.0.5.gem
Fetching rexml-3.2.5.gem
Fetching kramdown-2.4.0.gem
Fetching kramdown-parser-gfm-1.1.0.gem
Fetching ffi-1.15.5.gem
Fetching rb-inotify-0.10.1.gem
Fetching rb-fsevent-0.11.1.gem
Fetching listen-3.7.1.gem
Fetching jekyll-watch-2.2.1.gem
Fetching sassc-2.4.0.gem
Fetching jekyll-sass-converter-2.2.0.gem
Fetching concurrent-ruby-1.1.10.gem
Fetching i18n-1.12.0.gem
Fetching http_parser.rb-0.8.0.gem
Fetching eventmachine-1.2.7.gem
Fetching em-websocket-0.5.3.gem
Fetching colorator-1.1.0.gem
Fetching jekyll-4.2.2.gem
Fetching public_suffix-4.0.7.gem
Fetching addressable-2.8.0.gem
Successfully installed unicode-display_width-1.8.0
Successfully installed terminal-table-2.0.0
Successfully installed safe_yaml-1.0.5
Successfully installed rouge-3.30.0
Successfully installed forwardable-extended-2.6.0
Successfully installed pathutil-0.16.2
Successfully installed mercenary-0.4.0
Successfully installed liquid-4.0.3
Successfully installed rexml-3.2.5
Successfully installed kramdown-2.4.0
Successfully installed kramdown-parser-gfm-1.1.0
Building native extensions. This could take a while...
ERROR:  Error installing jekyll:
	ERROR: Failed to build gem native extension.

    current directory: /home/dami/.local/share/gem/ruby/gems/ffi-1.15.5/ext/ffi_c
/usr/bin/ruby -I /usr/share/rubygems -r ./siteconf20220817-13722-4dl25g.rb extconf.rb
mkmf.rb can't find header files for ruby at /usr/share/include/ruby.h

You might have to install separate package for the ruby development
environment, ruby-dev or ruby-devel for example.

extconf failed, exit code 1

Gem files will remain installed in /home/dami/.local/share/gem/ruby/gems/ffi-1.15.5 for inspection.
Results logged to /home/dami/.local/share/gem/ruby/extensions/x86_64-linux/3.1.0/ffi-1.15.5/gem_make.out
1 gem installed
```

- 여기서 잠깐! 페도라에서 yum 과 dnf 는 어떻게 다를까? 지금까지는 dnf 만 써왔는데..
- 그냥 dnf 가 yum 이 개선되어서 최근에 주로 사용되는 것이라고 한다.
- 그리고 여기서(https://try.ruby-lang.org/) 루비를 간단하게 테스트 해볼 수 있다! 재밌어 보이는데 시간이 나면 나중에 해보기로..

```ruby
3.times do
  print 'Welcome '
end
# Welcome Welcome Welcome 
```



2. ruby, ruby-dev, ruby-devel 설치

- ruby 와 RubyGem 간단 정리
    - Ruby 는 프로그래밍 언어 이고 가령 리눅스에 rpm나 deb 등 같은 Gem 은 라이브러리 라고 생각하면 된다.
    - 그리고 RubyGem 은 apt-get, dnf 같은 패키지 매니저 정도 되는 것 같다.

```bash
[dami@fedora install]$ ruby -v
ruby 3.1.2p20 (2022-04-12 revision 4491bb740a) [x86_64-linux]
[dami@fedora install]$ sudo dnf install ruby-devel
Installed:
  ruby-devel-3.1.2-164.fc36.x86_64  
```

- 다시 gem install bundler jekyll

```bash
gem install bundler jekyll

make: g++: No such file or directory
make: *** [Makefile:239: ast.o] Error 127

make failed, exit code 2

Gem files will remain installed in /home/dami/.local/share/gem/ruby/gems/sassc-2.4.0 for inspection.
Results logged to /home/dami/.local/share/gem/ruby/extensions/x86_64-linux/3.1.0/sassc-2.4.0/gem_make.out
1 gem installed
```
- make 와 g++ 명령어 를 제공하는 gcc-c++ 패키지 설치

```bash
make: *** No targets specified and no makefile found.  Stop.
[dami@fedora install]$ g++
bash: g++: command not found...
Install package 'gcc-c++' to provide command 'g++'? [N/y] y
Last metadata expiration check: 0:19:33 ago on Wed 17 Aug 2022 07:44:59 PM KST.
Package gcc-c++-12.1.1-1.fc36.x86_64 is already installed.
Dependencies resolved.
Nothing to do.
Complete!

```

- 다시 gem install bundler jekyll

```bash
[dami@fedora install]$ gem install bundler jekyll
Successfully installed bundler-2.3.20
Parsing documentation for bundler-2.3.20
Done installing documentation for bundler after 0 seconds
Building native extensions. This could take a while...
Successfully installed sassc-2.4.0
Successfully installed jekyll-sass-converter-2.2.0
Successfully installed concurrent-ruby-1.1.10
Successfully installed i18n-1.12.0
Building native extensions. This could take a while...
Successfully installed http_parser.rb-0.8.0
Building native extensions. This could take a while...
Successfully installed eventmachine-1.2.7
Successfully installed em-websocket-0.5.3
Successfully installed colorator-1.1.0
Successfully installed public_suffix-4.0.7
Successfully installed addressable-2.8.0
Successfully installed jekyll-4.2.2
Parsing documentation for sassc-2.4.0
Installing ri documentation for sassc-2.4.0
Parsing documentation for jekyll-sass-converter-2.2.0
Installing ri documentation for jekyll-sass-converter-2.2.0
Parsing documentation for concurrent-ruby-1.1.10
Installing ri documentation for concurrent-ruby-1.1.10
Parsing documentation for i18n-1.12.0
Installing ri documentation for i18n-1.12.0
Parsing documentation for http_parser.rb-0.8.0
unknown encoding name "chunked\r\n\r\n25" for ext/ruby_http_parser/vendor/http-parser-java/tools/parse_tests.rb, skipping
Installing ri documentation for http_parser.rb-0.8.0
Parsing documentation for eventmachine-1.2.7
Installing ri documentation for eventmachine-1.2.7
Parsing documentation for em-websocket-0.5.3
Installing ri documentation for em-websocket-0.5.3
Parsing documentation for colorator-1.1.0
Installing ri documentation for colorator-1.1.0
Parsing documentation for public_suffix-4.0.7
Installing ri documentation for public_suffix-4.0.7
Parsing documentation for addressable-2.8.0
Installing ri documentation for addressable-2.8.0
Parsing documentation for jekyll-4.2.2
Installing ri documentation for jekyll-4.2.2
Done installing documentation for sassc, jekyll-sass-converter, concurrent-ruby, i18n, http_parser.rb, eventmachine, em-websocket, colorator, public_suffix, addressable, jekyll after 8 seconds
12 gems installed
```

- 드디어 오류 없이 성공!

- 그리고 이제

- bundle exec jekyll serve 가 잘 되는지 확인..

- 페도라 dnf 패키지 관리가 너무 완벽하고 보기에도 너무 깔끔하다..페도라를 좋아하는 이유 중 하나..
![](2022-08-17-jekyllonfedora/Screenshot%20from%202022-08-17%2020-26-18.png)
![](2022-08-17-jekyllonfedora/Screenshot%20from%202022-08-17%2019-06-28.png)

```bash
[dami@fedora site]$ bundle exec jekyll serve
bundler: command not found: jekyll
Install missing gem executables with `bundle install`
```
- bundle install

```bash
[dami@fedora site]$ bundle install
Bundler 2.3.20 is running, but your lockfile was generated with 2.3.16. Installing Bundler 2.3.16 and restarting using that version.
Fetching gem metadata from https://rubygems.org/.
Fetching bundler 2.3.16
Installing bundler 2.3.16
Ignoring commonmarker-0.23.5 because its extensions are not built. Try: gem pristine commonmarker --version 0.23.5
Ignoring eventmachine-1.2.7 because its extensions are not built. Try: gem pristine eventmachine --version 1.2.7
Ignoring http_parser.rb-0.8.0 because its extensions are not built. Try: gem pristine http_parser.rb --version 0.8.0
Ignoring wdm-0.1.1 because its extensions are not built. Try: gem pristine wdm --version 0.1.1
Fetching gem metadata from https://rubygems.org/.........
Resolving dependencies...
Using bundler 2.3.16
Using ruby2_keywords 0.0.5
Using faraday-net_http 3.0.0
Using forwardable-extended 2.6.0
Fetching unf_ext 0.0.8.2
Using coffee-script-source 1.11.1
Using execjs 2.8.1
Using colorator 1.1.0
Using racc 1.6.0
Using gemoji 3.0.1
Using jekyll-paginate 1.1.0
Using rubyzip 2.3.2
Using multi_json 1.15.0
Using unicode-display_width 1.8.0
Using rexml 3.2.5
Using webrick 1.7.0
Using mercenary 0.3.6
Using pathutil 0.16.2
Using safe_yaml 1.0.5
Using rb-fsevent 0.11.1
Using concurrent-ruby 1.1.10
Fetching nokogiri 1.13.8 (x86_64-linux)
Using kramdown 2.3.2
Using jekyll-swiss 1.0.0
Using i18n 0.9.5
Using liquid 4.0.3
Using faraday 2.5.2
Using rouge 3.26.0
Using activesupport 3.2.22.5
Using katex 0.9.0
Using terminal-table 1.8.0
Fetching ffi 1.15.5
Using public_suffix 4.0.7
Using jekyll-mermaid 1.0.0
Using kramdown-parser-gfm 1.1.0
Using coffee-script 2.4.1
Using kramdown-math-katex 1.0.1
Using addressable 2.8.0
Using jekyll-coffeescript 1.1.1
Using sawyer 0.9.2
Using octokit 4.25.1
Using jekyll-gist 1.5.0
Installing commonmarker 0.23.5 with native extensions
It is a security vulnerability to allow your home directory to be world-writable, and bundler can not continue.
You should probably consider fixing this issue by running `chmod o-w ~` on *nix.
Please refer to https://ruby-doc.org/stdlib-2.1.2/libdoc/fileutils/rdoc/FileUtils.html#method-c-remove_entry_secure for details.
Installing http_parser.rb 0.8.0 with native extensions
Installing eventmachine 1.2.7 with native extensions
Installing unf_ext 0.0.8.2 with native extensions
Installing ffi 1.15.5 with native extensions
Installing nokogiri 1.13.8 (x86_64-linux)
Bundler::PathError: Please fix the world-writable issue with your /javatest/blog/site/vendor/bundle/ruby/3.1.0/gems/commonmarker-0.23.5 directory
  /javatest/blog/site/vendor/bundle/ruby/3.1.0/gems/bundler-2.3.16/lib/bundler.rb:339:in `rescue in rm_rf'
  /javatest/blog/site/vendor/bundle/ruby/3.1.0/gems/bundler-2.3.16/lib/bundler.rb:330:in `rm_rf'
  /javatest/blog/site/vendor/bundle/ruby/3.1.0/gems/bundler-2.3.16/lib/bundler/rubygems_gem_installer.rb:104:in `strict_rm_rf'
  /javatest/blog/site/vendor/bundle/ruby/3.1.0/gems/bundler-2.3.16/lib/bundler/rubygems_gem_installer.rb:19:in `install'
  /javatest/blog/site/vendor/bundle/ruby/3.1.0/gems/bundler-2.3.16/lib/bundler/source/rubygems.rb:207:in `install'
  /javatest/blog/site/vendor/bundle/ruby/3.1.0/gems/bundler-2.3.16/lib/bundler/installer/gem_installer.rb:54:in `install'
  /javatest/blog/site/vendor/bundle/ruby/3.1.0/gems/bundler-2.3.16/lib/bundler/installer/gem_installer.rb:16:in `install_from_spec'
  /javatest/blog/site/vendor/bundle/ruby/3.1.0/gems/bundler-2.3.16/lib/bundler/installer/parallel_installer.rb:186:in `do_install'
  /javatest/blog/site/vendor/bundle/ruby/3.1.0/gems/bundler-2.3.16/lib/bundler/installer/parallel_installer.rb:177:in `block in worker_pool'
  /javatest/blog/site/vendor/bundle/ruby/3.1.0/gems/bundler-2.3.16/lib/bundler/worker.rb:62:in `apply_func'
  /javatest/blog/site/vendor/bundle/ruby/3.1.0/gems/bundler-2.3.16/lib/bundler/worker.rb:57:in `block in process_queue'
  /javatest/blog/site/vendor/bundle/ruby/3.1.0/gems/bundler-2.3.16/lib/bundler/worker.rb:54:in `loop'
  /javatest/blog/site/vendor/bundle/ruby/3.1.0/gems/bundler-2.3.16/lib/bundler/worker.rb:54:in `process_queue'
  /javatest/blog/site/vendor/bundle/ruby/3.1.0/gems/bundler-2.3.16/lib/bundler/worker.rb:91:in `block (2 levels) in create_threads'

An error occurred while installing commonmarker (0.23.5), and Bundler cannot continue.

In Gemfile:
  github-pages was resolved to 227, which depends on
    jekyll-commonmark-ghpages was resolved to 0.2.0, which depends on
      jekyll-commonmark was resolved to 1.4.0, which depends on
        commonmarker
```


- 이후에 그냥 gemfile.lock 과 vendor 폴더를 지웟다..다시 bundle install

- 근데 잠깐. 여기에 메모

```
/usr/local/lib/ruby/2.7.0/rubygems/dependency.rb:311:in `to_specs': Could not find 'jekyll-theme-hydejack' (>= 0) among 148 total gem(s) (Gem::MissingSpecError)
Checked in 'GEM_PATH=/github/home/.gem/ruby/2.7.0:/usr/local/lib/ruby/gems/2.7.0:/usr/local/bundle', execute `gem env` for more information
```

- 깃헙 별도의 배쉬 창에서 push 하니 계속 패스워드 묻는 현상.
```
[dami@fedora site]$ ssh -T git@github.com  
Hi appstew! You've successfully authenticated, but GitHub does not provide shell access.
```

- https://mkyong.com/git/github-keep-asking-for-username-password-when-git-push/
```
The main reason for this problem is mistakenly git clone the HTTPS URL; we need the SSH URL to use the SSH keys. The solution is to update the .git/config file, url value to SSH instead of HTTPS.

2.1 Go to the repo directory, open the file .git/config.
2.2 Update the url from HTTPS https://github.com/mkyong/spring-boot to SSH git@github.com:mkyong/spring-boot.git.
```


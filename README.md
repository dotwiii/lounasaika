## lounasaika.net

### General instructions for contributing

1. [Fork](https://github.com/paav-o/lounasaika/fork_select) the repository
2. Clone your fork ``git clone https://github.com/your-user-name/lounasaika.git``
3. Commit your changes ``git commit -am 'Some description'``
4. Push commits ``git push origin master``
5. Send a [pull request](https://github.com/paav-o/lounasaika/pull/new/master)

### Contribute by updating restaurant opening times

Edit opening times or other information in ``config/restaurants.yml``

### Contribute by adding a new restaurant

As a prerequisite, you'll need to have Ruby with RubyGems installed: ``curl -L https://get.rvm.io | bash -s stable --ruby``

Navigate to project dir and install bundled gems: ``bundle``

Run ``rake new_restaurant`` and follow instructions.

### Updating using cron

*~/dev/update_lounasaika.sh*
```
#!/bin/bash

cd /home/users/paavo/dev/lounasaika
source /home/users/paavo/.rvm/environments/default
git checkout gh-pages
git pull
git checkout master
git pull
bundle install --quiet
bundle exec rake update
git add -A
git commit -m "Update by bot"
git push
bundle exec rake publish
```

```
$ chmod +x update_lounasaika.sh
$ crontab -e
```

```
5 0,7,10 * * 1 /home/users/paavo/dev/update_lounasaika.sh
```
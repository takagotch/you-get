### you-get
---
https://github.com/soimort/you-get

https://you-get.org/

```py
// src/you_get/__main__.py

_options = [
  'help',
  'version',
  'gui',
  'force',
  'playlists'
]
_short_options = 'hVgfl'

_help = """Usage: {} [OPTION]...[URL]...
TODO
""".format(script_name)

def main_dev(**kwargs):
  """
  """
  head = git.get_head(kwargs['repo_path'])
  
  try:
    opts, args = getopt.getopt(sys.argv[1:], _short_options, _options)
  except getopt.GetoptError as e:
    log.wtf("""
  [Fatal] {}.
  Try '{} --help' for more optoins.""".format(e, script_name))
  
  if not opts and not args:
    print(_help)
  else:
    conf = {}
    for opt, arg in opts:
      if opt in ('-h', '--help'):
        print(_help)
        
    elif opt in ('-V', '-version'):
      log.println("you-get:", log.BOLD)
      log.println("  version: {}".format(__version__))
      if head is not None:
        log.println(" branch: {}\n    commit: {}".format(*head))
      else:
        log.println("  branch: {}\n    commit: {}".format("(stable)", "(tag v{})".format(__version__)))
        
      log.println("  platform: {}".format(platform.platform()))
      log.println("  python: {}".format(sys.version.split('\n')[0]))
      
    elif opt in ('-g', '--gui'):
      conf['gui'] = True
      
    elif opt in ('-f', '--force'):
      conf['force'] = True
      
    elif opt in ('-l', '--playlist', '--playlists'):
      conf['playlist'] = True
      
  if args:
    if 'gui' in conf and conf['gui']:
      from .gui import gui_main
      gui_main(*args, **conf)
    else: 
      from .console import console_main
      console_main(*args, **conf)
      
def main(**kwargs):
  """
  """
  from .common import main
  main(**kwargs)
  
if __name__ == '__main__':
  main()
    
    
```

```
```

```
```


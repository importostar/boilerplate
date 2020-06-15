---
title: plumbum
date: 2020-05-07
---
Example Python program plumbum.py

## Modules

* from plumbum import cli
* from plumbum import local
* from plumbum.cmd import grep, cat

## Classes

* #   class GeetCommit(cli.Application):
* class Checker(cli.Application):
* class checkModuleVersion(cli.Application):

## Methods

*   def main(self, *arglist):

## Code

Python example

    ###########################################################
    # Application类 cli.Application
    #   - 命令选项 --> 成员变量 
    #        cli.Flag(["v", "verbose"], help = "help....")
    #   - 命令选项--> 修饰函数
    #       @cli.switch("--log-to-file", str)
    #       @cli.switch("--files", str, list=True, mandatory = True, requires = ["--依赖选项"])
    #   - 环境变量
    #       log_file = cli.SwitchAttr("--log-file", str, envname="MY_LOG_FILE")
    #   - 配置文件:
    #       with cli.Config('~/.myapp_rc') as conf
    #   - 子命令
    #       @Geet.subcommand("commit")
    #       class GeetCommit(cli.Application):
    #   - 主函数:
    # 	    Application::main(self, filename)
    
    #   - 属性:
    #       名称、版本:  PROGNAME, VERSION, DESCRIPTION
    #   - 调用: 
    #       cli.Application.run()
    ###########################################################
    from plumbum import cli
    class Checker(cli.Application):
      verbose = cli.Flag(["-v", "--verbose"], help = "Enable verbose mode")
    
    ###########################################
    # 子命令:
    #  - parent：指向ancestor.
    ###########################################
    @Checker.subcommand("module_version")
    class checkModuleVersion(cli.Application):
        “”“ 文档 ”“”
        # 里面可以嵌套参数。
        pass
       
      def main(self, *arglist):
        pass
    
    if __name__=="__main__":
      Checker.run()
    
      
    ##############################################################
    # shell command
    ##############################################################
    from plumbum import local
    ls = local["ls"]
    
    from plumbum.cmd import grep, cat
    
    # 指定路径生成
    pandoc = local.get('pandoc',
                       '~/AppData/Local/Pandoc/pandoc.exe',
                       '/Program Files/Pandoc/pandoc.exe',
                       '/Program Files (x86)/Pandoc/pandoc.exe')
    
    #############################################################
    # - 终端color支持:
    #   - colors.green | "ok"
    # - 进度条
    #   - for i in Progress.range(10):
    # - 图像显示 (效果太差 :<) 
    #   - python -m plumbum.cli.image myimage.png  (依赖pipenv install pillow)
    #   - cli.image.Image().show_pil(im)
    #############################################################
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

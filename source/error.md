---
title: error
date: 2020-05-07
---
Example Python program error.py


## Code

Python example

    
    Feb 06 17:37:02 martine-dedi python[10394]: Ignoring exception in on_message
    Feb 06 17:37:02 martine-dedi python[10394]: Traceback (most recent call last):
    Feb 06 17:37:02 martine-dedi python[10394]:   File "/home/kenny/redenv/lib/python3.8/site-packages/discord/client.py", line 312, in _run_event
    Feb 06 17:37:02 martine-dedi python[10394]:     await coro(*args, **kwargs)
    Feb 06 17:37:02 martine-dedi python[10394]:   File "/home/kenny/redenv/lib/python3.8/site-packages/redbot/core/events.py", line 266, in on_message
    Feb 06 17:37:02 martine-dedi python[10394]:     await bot.process_commands(message)
    Feb 06 17:37:02 martine-dedi python[10394]:   File "/home/kenny/redenv/lib/python3.8/site-packages/redbot/core/bot.py", line 838, in process_commands
    Feb 06 17:37:02 martine-dedi python[10394]:     await self.invoke(ctx)
    Feb 06 17:37:02 martine-dedi python[10394]:   File "/home/kenny/redenv/lib/python3.8/site-packages/discord/ext/commands/bot.py", line 892, in invoke
    Feb 06 17:37:02 martine-dedi python[10394]:     await ctx.command.invoke(ctx)
    Feb 06 17:37:02 martine-dedi python[10394]:   File "/home/kenny/redenv/lib/python3.8/site-packages/redbot/core/commands/commands.py", line 793, in invoke
    Feb 06 17:37:02 martine-dedi python[10394]:     await super().invoke(ctx)
    Feb 06 17:37:02 martine-dedi python[10394]:   File "/home/kenny/redenv/lib/python3.8/site-packages/discord/ext/commands/core.py", line 1217, in invoke
    Feb 06 17:37:02 martine-dedi python[10394]:     await self.prepare(ctx)
    Feb 06 17:37:02 martine-dedi python[10394]:   File "/home/kenny/redenv/lib/python3.8/site-packages/redbot/core/commands/commands.py", line 470, in prepare
    Feb 06 17:37:02 martine-dedi python[10394]:     await self.call_before_hooks(ctx)
    Feb 06 17:37:02 martine-dedi python[10394]:   File "/home/kenny/redenv/lib/python3.8/site-packages/discord/ext/commands/core.py", line 707, in call_before_hooks
    Feb 06 17:37:02 martine-dedi python[10394]:     await hook(ctx)
    Feb 06 17:37:02 martine-dedi python[10394]:   File "/home/kenny/bb/Red-DiscordBot/cogs/CogManager/cogs/audiobb8/audio.py", line 214, in cog_before_invoke
    Feb 06 17:37:02 martine-dedi python[10394]:     global_daily_playlists = self._daily_global_playlist_cache.setdefault(
    Feb 06 17:37:02 martine-dedi python[10394]: AttributeError: 'Audio' object has no attribute '_daily_global_playlist_cache'
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/

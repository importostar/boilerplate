---
title: History
date: 2020-05-07
---
Example Python program History.py


## Code

Python example

    [17/04/2019 15:14] INFO manager maybe_download_lavalink 161: Downloading Lavalink.jar
    Heartbeat blocked for more than 5 seconds.
    Unexpected exception in keepalive ping task
    Traceback (most recent call last):
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\websockets\protocol.py", line 989, in keepalive_ping
        ping_waiter, self.ping_timeout, loop=self.loop
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\asyncio\tasks.py", line 416, in wait_for
        return fut.result()
    websockets.exceptions.ConnectionClosed: WebSocket connection is closed: code = 1006 (connection closed abnormally [internal]), no reason
    Attempting a reconnect in 0.96s
    Traceback (most recent call last):
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\discord\gateway.py", line 483, in poll_event
        msg = await self.recv()
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\websockets\protocol.py", line 434, in recv
        yield from self.ensure_open()
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\websockets\protocol.py", line 646, in ensure_open
        ) from self.transfer_data_exc
    websockets.exceptions.ConnectionClosed: WebSocket connection is closed: code = 1000 (OK), no reason
    
    The above exception was the direct cause of the following exception:
    
    Traceback (most recent call last):
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\discord\client.py", line 410, in connect
        await self._connect()
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\discord\shard.py", line 284, in _connect
        f.result()
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\discord\shard.py", line 78, in poll
        await self.ws.poll_event()
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\discord\gateway.py", line 493, in poll_event
        raise ConnectionClosed(exc, shard_id=self.shard_id) from exc
    discord.errors.ConnectionClosed: WebSocket connection is closed: code = 1000 (OK), no reason
    [17/04/2019 15:17] INFO manager maybe_download_lavalink 161: Downloading Lavalink.jar
    [17/04/2019 15:17] INFO manager maybe_download_lavalink 161: Downloading Lavalink.jar
    [17/04/2019 15:17] INFO manager maybe_download_lavalink 161: Downloading Lavalink.jar
    Shard ID 0 has stopped responding to the gateway. Closing and restarting.
    [17/04/2019 15:22] ERROR core_commands _load 108: Package loading failed
    Traceback (most recent call last):
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\redbot\core\core_commands.py", line 104, in _load
        await bot.load_extension(spec)
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\redbot\core\bot.py", line 239, in load_extension
        await lib.setup(self)
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\redbot\cogs\audio\__init__.py", line 26, in setup
        await maybe_download_lavalink(bot.loop, cog)
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\redbot\cogs\audio\manager.py", line 164, in maybe_download_lavalink
        await download_lavalink(session)
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\redbot\cogs\audio\manager.py", line 148, in download_lavalink
        chunk = await resp.content.read(512)
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\aiohttp\streams.py", line 369, in read
        await self._wait('read')
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\aiohttp\streams.py", line 297, in _wait
        await waiter
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\aiohttp\helpers.py", line 585, in __exit__
        raise asyncio.TimeoutError from None
    concurrent.futures._base.TimeoutError
    Heartbeat blocked for more than 5 seconds.
    [17/04/2019 15:23] ERROR core_commands _load 108: Package loading failed
    Traceback (most recent call last):
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\redbot\core\core_commands.py", line 104, in _load
        await bot.load_extension(spec)
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\redbot\core\bot.py", line 239, in load_extension
        await lib.setup(self)
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\redbot\cogs\audio\__init__.py", line 26, in setup
        await maybe_download_lavalink(bot.loop, cog)
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\redbot\cogs\audio\manager.py", line 164, in maybe_download_lavalink
        await download_lavalink(session)
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\redbot\cogs\audio\manager.py", line 148, in download_lavalink
        chunk = await resp.content.read(512)
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\aiohttp\streams.py", line 369, in read
        await self._wait('read')
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\aiohttp\streams.py", line 297, in _wait
        await waiter
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\aiohttp\helpers.py", line 585, in __exit__
        raise asyncio.TimeoutError from None
    concurrent.futures._base.TimeoutError
    [17/04/2019 15:23] ERROR core_commands _load 108: Package loading failed
    Traceback (most recent call last):
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\redbot\core\core_commands.py", line 104, in _load
        await bot.load_extension(spec)
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\redbot\core\bot.py", line 239, in load_extension
        await lib.setup(self)
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\redbot\cogs\audio\__init__.py", line 26, in setup
        await maybe_download_lavalink(bot.loop, cog)
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\redbot\cogs\audio\manager.py", line 164, in maybe_download_lavalink
        await download_lavalink(session)
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\redbot\cogs\audio\manager.py", line 148, in download_lavalink
        chunk = await resp.content.read(512)
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\aiohttp\streams.py", line 369, in read
        await self._wait('read')
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\aiohttp\streams.py", line 297, in _wait
        await waiter
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\aiohttp\helpers.py", line 585, in __exit__
        raise asyncio.TimeoutError from None
    concurrent.futures._base.TimeoutError
    [17/04/2019 15:23] ERROR core_commands _load 108: Package loading failed
    Traceback (most recent call last):
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\redbot\core\core_commands.py", line 104, in _load
        await bot.load_extension(spec)
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\redbot\core\bot.py", line 239, in load_extension
        await lib.setup(self)
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\redbot\cogs\audio\__init__.py", line 26, in setup
        await maybe_download_lavalink(bot.loop, cog)
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\redbot\cogs\audio\manager.py", line 164, in maybe_download_lavalink
        await download_lavalink(session)
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\redbot\cogs\audio\manager.py", line 148, in download_lavalink
        chunk = await resp.content.read(512)
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\aiohttp\streams.py", line 369, in read
        await self._wait('read')
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\aiohttp\streams.py", line 297, in _wait
        await waiter
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\site-packages\aiohttp\helpers.py", line 585, in __exit__
        raise asyncio.TimeoutError from None
    concurrent.futures._base.TimeoutError
    Shard ID 0 has stopped responding to the gateway. Closing and restarting.
    Fatal read error on pipe transport
    protocol: <asyncio.sslproto.SSLProtocol object at 0x00000210C30CA6D8>
    transport: <_ProactorSocketTransport fd=924>
    Traceback (most recent call last):
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\asyncio\proactor_events.py", line 255, in _loop_reading
        data = fut.result()
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\asyncio\windows_events.py", line 744, in _poll
        value = callback(transferred, key, ov)
      File "C:\Users\RAJ\AppData\Local\Programs\Python\Python37\lib\asyncio\windows_events.py", line 435, in finish_recv
        return ov.getresult()
    OSError: [WinError 121] The semaphore timeout period has expired
    Heartbeat blocked for more than 5 seconds.

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

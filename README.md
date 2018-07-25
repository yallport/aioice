# aioice


## Interactive Connectivity Establishment (RFC 5245) 🔗


ICE using [jlaine's aioice library](https://github.com/jlaine/aioice). 

I edited the code so that the terminal outputs are more "pretty." Candidates are organized and in a different color, and the connection messages are more obvious.

aioice is a library for Interactive Connectivity Establishment (RFC 5245) in Python. It is built on top of asyncio, Python's standard asynchronous I/O framework.

Interactive Connectivity Establishment (ICE) is useful for applications that establish peer-to-peer UDP data streams, as it facilitates NAT traversal. Typical usecases include SIP and WebRTC.

aioice [Documentation](https://aioice.readthedocs.io/en/stable/)


## Example


    #!/usr/bin/env python

    import asyncio
    import aioice

    async def connect_using_ice():
        connection = aioice.Connection(ice_controlling=True)

        # gather local candidates
        await connection.gather_candidates()

        # send your information to the remote party using your signaling method
        send_local_info(
            connection.local_candidates,
            connection.local_username,
            connection.local_password)

        # receive remote information using your signaling method
        remote_candidates, remote_username, remote_password = get_remote_info()

        # perform ICE handshake
        connection.remote_candidates = remote_candidates
        connection.remote_username = remote_username
        connection.remote_password = remote_password
        await connection.connect()

        # send and receive data
        await connection.sendto(b'1234', 1)
        data, component = await connection.recvfrom()

        # close connection
        await connection.close()

    asyncio.get_event_loop().run_until_complete(connect_using_ice())



## License


aioice is released under the [BSD license](https://aioice.readthedocs.io/en/stable/license.html).

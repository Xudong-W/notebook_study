常见的并发网络服务器程序设计方案

accept+fork()  : one process per connection
	It is difficult to implement fork() properly
	dynamic linking versus static linking
		Another important fork performance factor is how much fork has to do.
		On modern platforms with a hardware memory management unit, fork only copies the page mappings.
		Dynamic linking creates many page mappings for the ELF sections in the shared libraries, and the Global Offset Table and so on.
		So, linking the fork benchmark statically ought to improve performance noticeably.

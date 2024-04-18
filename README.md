# MapReduce System Implementation in Go

## Introduction
In this lab, you'll build a MapReduce system, similar to the one described in the MapReduce paper. You'll implement a worker process that calls application Map and Reduce functions, handles file I/O, and a coordinator process that distributes tasks to workers and manages failures. This README guides you through the setup and implementation of the system.

## Getting Started
To begin, you'll need to set up Go for the lab exercises. Follow these steps to fetch the initial lab software using git:

```bash
$ git clone git://g.csail.mit.edu/6.5840-golabs-2024 6.5840
$ cd 6.5840
$ ls
Makefile src
```

## Lab Structure
We provide you with a sequential MapReduce implementation in `src/main/mrsequential.go`, along with sample MapReduce applications like word-count and a text indexer in `mrapps/`. You can run the word count sequentially as follows:

```bash
$ cd ~/6.5840/src/main
$ go build -buildmode=plugin ../mrapps/wc.go
$ rm mr-out*
$ go run mrsequential.go wc.so pg*.txt
$ more mr-out-0
```

Feel free to explore the provided code in `mrsequential.go` and `mrapps/wc.go`.

## Your Job
Your task is to implement a distributed MapReduce system, comprising a coordinator and worker programs. The coordinator assigns tasks to workers, manages task failures, and ensures job completion. Workers execute Map and Reduce functions, handle file I/O, and communicate with the coordinator via RPC. Follow the instructions in the lab write-up to complete the implementation.

## Running Your Code
You can test your implementation with the provided MapReduce applications. Follow these steps to run the word-count application:

```bash
$ go build -buildmode=plugin ../mrapps/wc.go
$ rm mr-out*
$ go run mrcoordinator.go pg-*.txt
```

In separate windows, run worker processes:

```bash
$ go run mrworker.go wc.so
```

Once completed, examine the output in `mr-out-*` files.

## Testing
We provide a test script `test-mr.sh` to verify the correctness of your implementation. Run it to ensure your system passes all required tests. For debugging and development tips, refer to the Guidance page.

## Additional Notes
- Ensure your code works with the original versions provided. You can add new functions or modify existing ones as directed.
- Pay attention to file naming conventions and output formats specified in the lab instructions.
- Utilize Go's built-in race detector for debugging (`go run -race`). However, your code should not contain race conditions for production.
- Consider the provided hints and suggestions for efficient implementation.

## Challenges (Optional)
- Implement your own MapReduce application.
- Configure your MapReduce system to run on separate machines with TCP/IP communication and a shared file system.

Follow the lab write-up for detailed instructions and guidelines. Happy coding!


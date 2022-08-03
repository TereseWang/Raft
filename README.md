# Raft 
Implementing the raft algorithm (explaination paper provided)
## High Level Approach

We followed the architecture described in the Raft paper provided on the project website. Each replica has a random election timeout (150ms - 300ms) and starts an election when the timeout is reached, changing its state to candidate, increment its term, and request votes from other replicas. When it receives a majority vote, it becomes the leader and immediately start sending heartbeat messages to other replicas to establish its authority. The heartbeat messages are sent at an interval of 100ms to prevent new election. If a candidate receives a heartbeat with a term higher than its term, it recognizes this replica as the new leader. Votes are casted with a first come first serve manner, and we maintain that each replica can only cast 1 vote for a single term. This structure worked for the 3 tests required by the milestone.

## Challenges

The biggest challange for this milestone is to implement the election logic. We modified the code gradually to achieve a working protocol. Some difficulties we faced were: deciding when to start an election, sending heartbeat messages at an interval that prevents new elections and does not send too many packets, correctly recognizing new leader and increment term.

## Testing

We used the test scripts provided on the project website and configured our own JSON tests to accommodate our own test cases. We also printed out important debug messages that helped us keep track of how the protocol is executed and locate bugs in our program. The program was ran on the Khoury Linux Machine and successfully passed the required tests for the milestone. 
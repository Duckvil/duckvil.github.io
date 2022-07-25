# Events

## Event types
Currently two types of events are supported: **buffered** and **immediate**.  
**Buffered** events are dispatched at a specific time and place, whereas **immediate** are dispatched right after broadcasting.

### Buffered events
Mandatory functions

#### Broadcast
Used for firing events.
```cpp
template <typename Message>
void Broadcast(const Message& _message);
```

#### AnyEvents
Check if any events are remaining.
```cpp
bool AnyEvents() const;
```

#### GetMessage
Returns **true** if remaining event type is the same as Message type.
```cpp
template <typename Message>
bool GetMessage(Message* _pMessage);
```

#### EventHandled
Use if event was handled successfully.

The event will be popped.
```cpp
template <typename Message>
void EventHandled();
```

Keep the event to the next frame.
```cpp
template <typename Message>
void EventHandled(const Message& _message);
```

#### Reset
```cpp
void Reset();
```

#### Clear
```cpp
void Clear();
```

#### Skip
```cpp
void Skip();
```

### Immediate events

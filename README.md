# Objective-C KVO Memory Management Bug

This repository demonstrates a subtle bug related to Key-Value Observing (KVO) and memory management in Objective-C.  The bug arises from failing to remove an observer before the observed object is deallocated, particularly when using weak references. This can lead to crashes or unpredictable behavior.

## Bug Description
The primary issue is the lack of proper cleanup.  An observer is added to an object but not removed when the object is no longer needed.  If the observed object gets deallocated while the observer still holds a weak reference, accessing the deallocated object will likely cause a crash.

## Solution
The solution involves ensuring that the `removeObserver:` method is called before the observed object is deallocated. This prevents potential crashes and undefined behavior associated with accessing memory that has already been freed.
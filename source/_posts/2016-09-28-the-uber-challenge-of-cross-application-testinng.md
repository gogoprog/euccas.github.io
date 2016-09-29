---
layout: post
title: "GTAC: The Uber Challenge of Cross-Application Testing"
date: 2016-09-28 23:17:30 -0700
comments: true
categories: GTAC infrastructure testing
---

Inspired by Matt Cutts' TED talk: [Try something new for 30 days](https://www.ted.com/talks/matt_cutts_try_something_new_for_30_days?language=en), I'm starting a 30-day-GTAC-revisit project. Google's Test Automation Conference [GTAC](https://developers.google.com/google-test-automation-conference/) is an annual test automation conference which brings together engineers from industry and academia to discuss advances in test automation and related engineering tools. In my 30-day-GTAC-revisit project, I'll review the topics presented on GTAC. My goal of the 30-day-GTAC-revisit project is having a better and deeper understanding in modern testing technologies, methodologies, strategies, and practices.

Get it started! Day#1 topic is:

**The Uber Challenge of Cross-Application/Cross-Device Testing**

- Presenter: Apple Chow (Uber), Bian Jiang (Uber)
- [Video](https://www.youtube.com/watch?v=p6gsssppeT0&list=PLSIUOFhnxEiCWGsN9t5A-XOhRbmz54IS1&index=3)
- [Slides](https://docs.google.com/presentation/d/1vYXhkvgLKun72Ix91LQDDWZQdcY5VOBqKVvI1Y6riYo/pub)

**My takeaways**

- The challenge: End-to-end tests require cross application communication (between rider app and driver app)
- Uber's solution: Octopus
	- Octopus coordinates communication across different apps running on different devices
	- This solution can be adopted for any tests that require coordination/communication across different apps or devices
- What makes testing Uber's mobile apps significantly different from testing Google Maps?
- Why Octopus? Unified. Extensible. Parallelized. Signaling.
- What does Octopus do? Prepare test targets. Run tests (handles signaling). Create test results reports. Pull test artifacts. Perform clean ups.
- Signaling between driver test and rider test: Conducted with Test Host. API readSignal (blocking), writeSignal (nonblocking)







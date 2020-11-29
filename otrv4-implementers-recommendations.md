# OTR version 4 recommendations for client implementers

```
Disclaimer

This protocol specification is a draft. It's currently under constant revision.
```

This document describes some recommendations for client implementers of the
[version 4 of the Off-the-Record Messaging protocol](https://github.com/otrv4/otrv4/blob/master/otrv4.md).
This document expands on what is described in the protocol and implementers
can decide if they follow them or not.

## Table of Contents

1. [Long-term key material advice](#main-changes-over-version-3)
   1. [Exporting/importing long-term keys](#conversation-started-by-an-interactive-dake)
   1. [Verification of long-term keys](#conversation-started-by-an-interactive-dake)
   1. [Forging keys and its private counterpart](#conversation-started-by-an-interactive-dake)
1. [Persistent values advice](#main-changes-over-version-3)
1. [Ephemeral key advice](#main-changes-over-version-3)
   1. [Working with the extra symmetric key](#conversation-started-by-an-interactive-dake)
1. [Double ratchet algorithm advice](#main-changes-over-version-3)
   1. [Defining Phi](#conversation-started-by-an-interactive-dake)
   1. [Test cases](#conversation-started-by-an-interactive-dake)
1. [Handling of data messages advice](#main-changes-over-version-3)
   1. [Handling TLV type 1 Disconnected](#conversation-started-by-an-interactive-dake)
   1. [Conversion of decrypted plaintext](#conversation-started-by-an-interactive-dake)
1. [Protocol state machine advice](#main-changes-over-version-3)
   1. [Handling delayed messages](#conversation-started-by-an-interactive-dake)
   1. [Queueing messages](#conversation-started-by-an-interactive-dake)
   1. [OTRv3 and OTRv4 state machine](#conversation-started-by-an-interactive-dake)
1. [OTRv4 policies advice](#main-changes-over-version-3)
   1. [Defining OTRv4 policies](#conversation-started-by-an-interactive-dake)
   1. [Working with instance tags](#conversation-started-by-an-interactive-dake)
1. [General OTRv4 advice](#main-changes-over-version-3)
   1. [Working with threads](#conversation-started-by-an-interactive-dake)
   1. [Handling chat history](#conversation-started-by-an-interactive-dake)

# OTRv4 policies advice

OTRv4 clients can set different policies for different correspondents. For
example, Alice could set up her client so that it speaks only OTR version 4,
except with Charlie, who she knows has only an old client; so that it will
opportunistically start an OTR conversation whenever it detects the
correspondent supports it; or so that it refuses to send non-encrypted messages
to Bob, ever.

Note that OTRv1 and OTRv2 are not supported anymore.

The policies that can be set (on a global or per-correspondent basis) are any
combination of the following boolean flags:

```
ALLOW_V3
  Allow version 3 of the OTR protocol to be used.

ALLOW_V4
  Allow version 4 of the OTR protocol to be used.

ALLOW_V34
  Allow version 3 and 4 of the OTR protocol to be used.

REQUIRE_ENCRYPTION
  Refuse to send unencrypted messages.

SEND_WHITESPACE_TAG
  Advertise your support of OTR(v3/v4) using the whitespace tag.

WHITESPACE_START_DAKE
  Start the OTRv4 DAKE when you receive a whitespace tag.
  Note that this should only start an interactive conversation.

ERROR_START_DAKE
  Start the OTR DAKE when you receive an OTRv4 Error Message.

OTRNG_REQUIRE_INTERACTIVE
  Only allow for OTRv4 interactive conversations. This should only be used
  for parties trying to send a message to someone who is offline.

OTRNG_IDENTITY_START_DAKE
  Allow that receiving a directly an identity message can start an interactive
  DAKE. It will only allow to start online conversations with it.

OTRNG_REQUIRE_AUTHENTICATED
  Allow to start offline or online OTRv4 conversations only when the party
  has been authenticated.
```

This policies can be advertised together or in groups.

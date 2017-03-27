---
layout: post
title:  "Adding attachments to a mailgun email deployment"
date:   2017-03-24 10:27:00
categories: blog
tags: mailgun api symfony
published: true
---

I had a request come in from a client about dispatching an email to a select list but it needed to include an attachment.  They were using mailgun and Symfony so I dived into the package to see how this would be done.  For reference, this was the package

	mailgun/mailgun-php

The documentation on github was good but not enough.  So I took a look at the package itself for an answer.  This was the sendMessage method:

	public function sendMessage($workingDomain, $postData, $postFiles = [])
    {
        if (is_array($postFiles)) {
            return $this->post("$workingDomain/messages", $postData, $postFiles);
        } elseif (is_string($postFiles)) {
            $tempFile = tempnam(sys_get_temp_dir(), 'MG_TMP_MIME');
            $fileHandle = fopen($tempFile, 'w');
            fwrite($fileHandle, $postFiles);

            $result = $this->post("$workingDomain/messages.mime", $postData, ['message' => $tempFile]);
            fclose($fileHandle);
            unlink($tempFile);

            return $result;
        } else {
            throw new Exceptions\MissingRequiredMIMEParameters(ExceptionMessages::EXCEPTION_MISSING_REQUIRED_MIME_PARAMETERS);
        }
    }

From here I can see it accepts an array of file attachments.  So in my controller, I added the full path of the file and it worked beautifully.






















## Description

Every email consists of a local name and a domain name, separated by the @ sign.

For example, in ``alice@leetcode.com``, ``alice`` is the local name, and ``leetcode.com`` is the domain name.

Besides lowercase letters, these emails may contain ``'.'``s or ``'+'`` s.

If you add periods (``'.'``) between some characters in the local name part of an email address, mail sent there will be forwarded to the same address without dots in the local name.  For example, ``"alice.z@leetcode.com" `` and ``"alicez@leetcode.com"`` forward to the same email address.  (Note that this rule does not apply for domain names.)

If you add a plus (``'+'``) in the local name, everything after the first plus sign will be ignored. This allows certain emails to be filtered, for example ``m.y+name@email.com`` will be forwarded to ``my@email.com``.  (Again, this rule does not apply for domain names.)

It is possible to use both of these rules at the same time.

Given a list of emails, we send one email to each address in the list.  How many different addresses actually receive mails?

**Example 1:**
```
Input: 
["test.email+alex@leetcode.com","test.e.mail+bob.cathy@leetcode.com","testemail+david@lee.tcode.com"]
Output: 2
Explanation: "testemail@leetcode.com" and "testemail@lee.tcode.com" actually receive mails
```

**Note:**

- 1 <= emails[i].length <= 100

- 1 <= emails.length <= 100

- Each emails[i] contains exactly one '@' character.

## Solutions

### My solution

```python
class Solution(object):
    def numUniqueEmails(self, emails):
        """
        :type emails: List[str]
        :rtype: int
        """
        id = set()
        for email in emails:
            email_split = email.split("@")
            local = email_split[0]
            if '.' in local:
                tmp = local.split('.')
                local = str(''.join(tmp))
            if '+' in local:
                local = local[:local.index('+')]
            id.add(local+email_split[1])
        return len(id)
```

题目中说了domain部分中两条规则都不适用，因此就直接将后半部分县先存起来备用，只看前半部分。既然点相当于没有，那么就直接去掉；加号后面都忽略，就只取前面半部分。
因此我使用了一个循环，做了上面说的几个操作最后将domain拼接起来存入集合中。最后返回集合长度。

### Solution 1
```python
class Solution(object):
    def numUniqueEmails(self, emails):
        seen = set()
        for email in emails:
            local, _, domain = email.partition('@')
            if '+' in local:
                local = local[:local.index('+')]
            seen.add(local.replace('.','') + '@' + domain)
        return len(seen)
```
官方给的答案还真是简洁。
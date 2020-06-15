---
title: test_unicode
date: 2020-05-07
---
Example Python program test_unicode.py

## Modules

* import sys
* import pytest

## Classes

* class TestLiteralStrings(object):
* class TestLength(object):
* class TestDefaultEncoding(object):
* class TestEncode(object):
* class TestDecode(object):
* class TestImplicitDecoding(object):
* class TestReadingFromFiles(object):

## Methods

* def test_in_python_2_literal_strings_are_byte_strings_by_default(self):
* def test_in_python_3_string_literals_are_unicode(self):
* def test_you_can_also_do_a_literal_byte_string_with_a_b_prefix(self):
* def test_literal_unicode_strings_have_u_prefix(self):
* def test_in_python_2_bytes_is_an_alias_for_str(self):
* def test_theres_no_type_called_unicode_in_python3(self):
* def test_the_length_of_a_unicode_string_is_its_number_of_code_points(self):
* def test_the_length_of_a_byte_string_is_its_number_of_bytes(self):
* def test_in_python_2_the_default_encoding_is_ascii(self):
* def test_in_python_3_the_default_encoding_is_uff8(self):
* def test_encoding_a_unicode_string_turns_it_into_a_byte_string(self):
* def test_encode_raises_UnicodeEncodeError(self):
* def test_in_python_2_you_can_encode_a_byte_string(self):
* def test_in_python_2_encoding_a_byte_string_can_raise_UnicodeDecodeError(self):
* def test_in_python_3_you_cant_encode_a_byte_string(self):
* def test_in_python_2_encoding_encodes_to_ascii_by_default(self):
* def test_you_can_tell_encode_to_replace_incompatible_chars_with_question_marks_instead_of_crashing(self):
* def test_you_can_tell_encode_to_replace_incompatible_chars_with_XML_instead_of_crashing(self):
* def test_you_can_tell_encode_to_omit_incompatible_chars_instead_of_crashing(self):
* def test_decoding_a_byte_string_turns_it_into_a_unicode_string(self):
* def test_decode_raises_UnicodeDecodeError(self):
* def test_decoding_a_utf8_string_as_ascii_will_work_if_there_are_no_non_ascii_chars(self):
* def test_decoding_using_the_wrong_encoding_sometimes_works(self, wrong_encoding):
* def test_decoding_with_utf8_can_also_raise_UnicodeDecodeError(self):
* def test_in_python_2_decode_decodes_from_ascii_by_default(self):
* def test_in_python_3_decode_decodes_from_utf8_by_default(self):
* def test_you_can_tell_decode_to_omit_incompatible_bytes(self):
* def test_you_can_tell_decode_to_replace_incompatible_bytes_with_question_marks(self):
* def test_in_python_2_concatenating_strings_implicitly_decodes_byte_strings_to_unicode_strings(self):
* def test_in_python_2_concatenating_strings_can_raise_UnicodeDecodeError(self):
* def test_in_python_3_you_cannot_concatenate_unicode_with_bytes(self):
* def test_in_python_2_formatting_strings_can_raise_UnicodeDecodeError(self):
* def test_python_3_calls_repr_when_you_format_byte_strings_into_unicode_strings(self):
* def test_in_python_3_you_cant_format_unicode_strings_into_byte_strings(self):
* def test_in_python_2_byte_strings_and_unicode_strings_can_be_equal(self):
* def test_in_python_3_byte_strings_and_unicode_strings_cannot_be_equal(self):
* def test_in_python_2_you_can_use_a_byte_string_to_match_a_unicode_dict_key(self):
* def test_in_python_3_you_cannot_use_a_byte_string_to_match_a_unicode_dict_key(self):
* def test_in_python_2_you_can_use_a_unicode_string_to_match_a_byte_string_dict_key(self):
* def test_in_python_3_you_cannot_use_a_unicode_string_to_match_a_byte_string_dict_key(self):
* def test_trying_to_encode_a_byte_string_implicitly_decodes_it_to_unicode_using_ascii_first(self):
* def test_in_python_2_reading_text_from_file_returns_bytes_by_default(self):
* def test_in_python_3_reading_text_from_file_returns_unicode_by_default(self):
* def test_you_can_read_bytes_from_file_too(self):

## Code

Python example

    # -*- coding: utf-8 -*-
    import sys
    
    import pytest
    
    is_python3 = sys.version_info[0] > 2
    
    if is_python3:
        unicode_type = str
        bytes_type   = bytes
    else:
        unicode_type = unicode
        bytes_type   = str
    
    # Skip tests marked @python2 if we're running in Python 3.
    python2 = pytest.mark.skipif(is_python3, reason="This test only works in Python 2")
    
    # Skip tests marked @python3 if we're running in Python 2.
    python3 = pytest.mark.skipif(not is_python3, reason="This test only works in Python 3")
    
    
    class TestLiteralStrings(object):
    
        @python2
        def test_in_python_2_literal_strings_are_byte_strings_by_default(self):
            # Each character in this string represents a byte (or sequence of bytes
            # for certain characters) in either ASCII or the encoding given in the
            # -*- coding comment at the top of the file.
            assert type("byte_string") == str
    
        @python3
        def test_in_python_3_string_literals_are_unicode(self):
            # The type of a string literal in Python 3 is "str", as in Python 2, but
            # in Python 3 "str" means a unicode string (sequence of unicode code
            # points) not a byte string (sequence of encoded bytes) as in Python 2!
            assert type("Hi") == str
    
        def test_you_can_also_do_a_literal_byte_string_with_a_b_prefix(self):
            assert type(b"byte_string") == bytes_type
    
        def test_literal_unicode_strings_have_u_prefix(self):
            # Each character in this string represents a code point.
            assert type(u"unicode_string") == unicode_type
    
        @python2
        def test_in_python_2_bytes_is_an_alias_for_str(self):
            assert bytes == str
    
        @python3
        def test_theres_no_type_called_unicode_in_python3(self):
            # There's no "unicode" type in Python 3 ("str" is the unicode type).
            with pytest.raises(NameError, match="^name 'unicode' is not defined"):
                unicode
    
    
    class TestLength(object):
    
        def test_the_length_of_a_unicode_string_is_its_number_of_code_points(self):
            assert len(u"Hi \u2119\u01b4\u2602\u210c\xf8\u1f24") == 9
    
        def test_the_length_of_a_byte_string_is_its_number_of_bytes(self):
            # The length of a byte string counts its number of bytes not its number
            # of "characters" or unicode code points.
            assert len(u"Hi \u2119\u01b4\u2602\u210c\xf8\u1f24".encode("utf-8")) == 19
    
    
    class TestDefaultEncoding(object):
    
        @python2
        def test_in_python_2_the_default_encoding_is_ascii(self):
            assert sys.getdefaultencoding() == "ascii"
    
        @python3
        def test_in_python_3_the_default_encoding_is_uff8(self):
            assert sys.getdefaultencoding() == "utf-8"
    
    
    class TestEncode(object):
    
        def test_encoding_a_unicode_string_turns_it_into_a_byte_string(self):
            byte_string = u"Hi \u2119\u01b4\u2602\u210c\xf8\u1f24".encode("utf-8")
    
            assert type(byte_string) == bytes_type
            assert byte_string == b'Hi \xe2\x84\x99\xc6\xb4\xe2\x98\x82\xe2\x84\x8c\xc3\xb8\xe1\xbc\xa4'
    
        def test_encode_raises_UnicodeEncodeError(self):
            # Not every encoding supports all possible unicode characters.
            # For example ASCII only supports ASCII chars.
            # If you try to encode a unicode string containing non-ASCII charas using
            # the ASCII encoding it'll raise UnicodeEncodeError.
            with pytest.raises(UnicodeEncodeError, match="^'ascii' codec can't encode character"):
                u"Hello ✋".encode("ascii")
    
        @python2
        def test_in_python_2_you_can_encode_a_byte_string(self):
            # Byte strings have an encode method in Python 2!
            # It implicitly decodes the byte string to unicode and then encodes
            # the unicode string.
            original_byte_string = b"hello"
    
            new_byte_string = original_byte_string.encode("utf-8")
    
            assert type(new_byte_string) == str
            assert new_byte_string == 'hello'
    
        @python2
        def test_in_python_2_encoding_a_byte_string_can_raise_UnicodeDecodeError(self):
            byte_string = b"Hi \u2119\u01b4\u2602\u210c\xf8\u1f24"
    
            with pytest.raises(UnicodeDecodeError):
                byte_string.encode("ascii")
    
        @python3
        def test_in_python_3_you_cant_encode_a_byte_string(self):
            byte_string = b"Hi \u2119\u01b4\u2602\u210c\xf8\u1f24"
    
            with pytest.raises(AttributeError):
                byte_string.encode("ascii")
    
        @python2
        def test_in_python_2_encoding_encodes_to_ascii_by_default(self):
            # By default encode() uses the system default encoding which is ascii.
            with pytest.raises(UnicodeEncodeError, match="^'ascii' codec can't encode character"):
                u"Hi \u2119\u01b4\u2602\u210c\xf8\u1f24".encode()
    
        def test_you_can_tell_encode_to_replace_incompatible_chars_with_question_marks_instead_of_crashing(self):
            unicode_string = u"Hi \u2119\u01b4\u2602\u210c\xf8\u1f24"
    
            byte_string = unicode_string.encode("ascii", "replace")
    
            assert byte_string == b"Hi ??????"
    
        def test_you_can_tell_encode_to_replace_incompatible_chars_with_XML_instead_of_crashing(self):
            unicode_string = u"Hi \u2119\u01b4\u2602\u210c\xf8\u1f24"
    
            byte_string = unicode_string.encode("ascii", "xmlcharrefreplace")
    
            # This output can actually be used in an XML or HTML file and will render
            # correctly in a browser.
            assert byte_string == b"Hi &#8473;&#436;&#9730;&#8460;&#248;&#7972;"
    
        def test_you_can_tell_encode_to_omit_incompatible_chars_instead_of_crashing(self):
            unicode_string = u"Hi \u2119\u01b4\u2602\u210c\xf8\u1f24"
    
            byte_string = unicode_string.encode("ascii", "ignore")
    
            assert byte_string == b"Hi "
    
    
    class TestDecode(object):
    
        def test_decoding_a_byte_string_turns_it_into_a_unicode_string(self):
            byte_string = b'Hi \xe2\x84\x99\xc6\xb4\xe2\x98\x82\xe2\x84\x8c\xc3\xb8\xe1\xbc\xa4'
    
            unicode_string = byte_string.decode("utf-8")
    
            assert type(unicode_string) == unicode_type
            assert unicode_string == u'Hi \u2119\u01b4\u2602\u210c\xf8\u1f24'
    
        def test_decode_raises_UnicodeDecodeError(self):
            utf8_byte_string = b"Hello \xe2\x9c\x8b"
    
            with pytest.raises(UnicodeDecodeError, match="^'ascii' codec can't decode byte"):
                utf8_byte_string.decode("ascii")
    
        def test_decoding_a_utf8_string_as_ascii_will_work_if_there_are_no_non_ascii_chars(self):
            # Since UTF8 is a super-set of ASCII, as long as the byte string doesn't
            # contain any non-ASCII characters then decoding a UTF8 string as ASCII
            # will work (but you should never do this!)
            utf8_byte_string = b"Hello :wave:"
    
            assert utf8_byte_string.decode("ascii") == u"Hello :wave:"
    
        @pytest.mark.parametrize("wrong_encoding", ("iso8859-1", "utf-16-le", "utf-16-be", "shift-jis"))
        def test_decoding_using_the_wrong_encoding_sometimes_works(self, wrong_encoding):
            utf8_byte_string = b'\x48\x69\xe2\x84\x99\xc6\xb4\xe2\x98\x82\xe2\x84\x8c\xc3\xb8\xe1\xbc\xa4'
            correct_unicode = utf8_byte_string.decode("utf-8")
    
            wrong_unicode = utf8_byte_string.decode(wrong_encoding)
    
            # The string decodes without error, but it produces the wrong code points,
            # the wrong string of characters. This is one way that you can end up
            # displaying garbage characters to users.
            assert wrong_unicode != correct_unicode
    
        def test_decoding_with_utf8_can_also_raise_UnicodeDecodeError(self):
            # Decoding a byte string using the UTF8 codec can also raise
            # UnicodeDecodeError, for example is the string is encoded using some
            # other encoding (neither UTF8 nor ASCII) or is just an invalid byte
            # string.
            with pytest.raises(UnicodeDecodeError, match="codec can't decode byte"):
                b"\x78\x9a\xbc\xde\xf0".decode("utf-8")
    
        @python2
        def test_in_python_2_decode_decodes_from_ascii_by_default(self):
            with pytest.raises(UnicodeDecodeError, match="^'ascii' codec can't decode byte"):
                b'Hi \xe2\x84\x99\xc6\xb4\xe2\x98\x82\xe2\x84\x8c\xc3\xb8\xe1\xbc\xa4'.decode()
    
        @python3
        def test_in_python_3_decode_decodes_from_utf8_by_default(self):
            with pytest.raises(UnicodeDecodeError, match="^'utf-8' codec can't decode byte"):
                b'\x78\x9a\xbc\xde\xf0'.decode()
    
        def test_you_can_tell_decode_to_omit_incompatible_bytes(self):
            utf8_byte_string = b"Hello \xe2\x9c\x8b"
    
            unicode_string = utf8_byte_string.decode("ascii", "ignore")
    
            assert unicode_string == u"Hello "
    
        def test_you_can_tell_decode_to_replace_incompatible_bytes_with_question_marks(self):
            utf8_byte_string = b"Hello \xe2\x9c\x8b"
    
            unicode_string = utf8_byte_string.decode("ascii", "replace")
    
            # In this case it uses a non-ASCII question mark code point.
            # Note that there are three ?'s here - one for every incompatible _byte_ in
            # the UTF8 byte string. The single ✋character is three bytes.
            assert unicode_string == u"Hello ���"
    
    
    class TestImplicitDecoding(object):
    
        @python2
        def test_in_python_2_concatenating_strings_implicitly_decodes_byte_strings_to_unicode_strings(self):
            # The byte string is implicitly decoded to a unicode string using the
            # system's default encoding (ascii by default).
            concatenated = u"Hello " + b"world"
    
            assert type(concatenated) == unicode_type
            assert concatenated == u"Hello world"
    
        @python2
        def test_in_python_2_concatenating_strings_can_raise_UnicodeDecodeError(self):
            with pytest.raises(UnicodeDecodeError, match="^'ascii' codec can't decode byte"):
                # The second string here us a UTF8 byte string containing a non-ASCII
                # character. Python will try to decode it to unicode using ASCII and
                # crash.
                u"Hello " + b"\xe2\x9c\x8b"
    
        @python3
        def test_in_python_3_you_cannot_concatenate_unicode_with_bytes(self):
            # Python 3 never tries to implicitly decode byte strings using a default
            # encoding when you try to concatenate them with unicode strings, format
            # them, etc.
            #
            # Instead, it explicitly refuses to let you do that.
            with pytest.raises(TypeError, match="^must be str, not bytes$"):
                "Hello " + b"world"
    
        @python2
        def test_in_python_2_formatting_strings_can_raise_UnicodeDecodeError(self):
            with pytest.raises(UnicodeDecodeError, match="^'ascii' codec can't decode byte"):
                u"Hello %s" % b"\xe2\x9c\x8b"
    
        @python3
        def test_python_3_calls_repr_when_you_format_byte_strings_into_unicode_strings(self):
            # Unlike, for example, the + operator the % operator (when used with
            # %s) will call str() on its argument.
            # 
            # In this case the argument is a byte string and str() on a byte string
            # just falls back on repr() which returns "b'\\xe1\\x9c\\x8b'".
            assert u'Hello %s' % b'\xe1\x9c\x8b' == u"Hello b'\\xe1\\x9c\\x8b'"
    
        @python3
        def test_in_python_3_you_cant_format_unicode_strings_into_byte_strings(self):
            with pytest.raises(TypeError, match="^%b requires a bytes-like object, or an object that implements __bytes__, not 'str'"):
                assert b'\xe1\x9c\x8b %s' % u"Hello"
    
        @python2
        def test_in_python_2_byte_strings_and_unicode_strings_can_be_equal(self):
            assert b"Hello" == u"Hello"
    
        @python3
        def test_in_python_3_byte_strings_and_unicode_strings_cannot_be_equal(self):
            assert b"Hello" != u"Hello"
    
        @python2
        def test_in_python_2_you_can_use_a_byte_string_to_match_a_unicode_dict_key(self):
            assert {u"hello": u"world"}[b"hello"] == u"world"
    
        @python3
        def test_in_python_3_you_cannot_use_a_byte_string_to_match_a_unicode_dict_key(self):
            with pytest.raises(KeyError):
                {u"hello": u"world"}[b"hello"]
    
        @python2
        def test_in_python_2_you_can_use_a_unicode_string_to_match_a_byte_string_dict_key(self):
            assert {b"hello": b"world"}[u"hello"] == b"world"
    
        @python3
        def test_in_python_3_you_cannot_use_a_unicode_string_to_match_a_byte_string_dict_key(self):
            with pytest.raises(KeyError):
                {b"hello": b"world"}[u"hello"]
    
        @python2
        def test_trying_to_encode_a_byte_string_implicitly_decodes_it_to_unicode_using_ascii_first(self):
            utf8_byte_string = "Hello ✋"
    
            # This is Python 2 trying to be even more "helpful". Even though it makes
            # no sense to call .encode() on an (already-encoded) byte string, if you
            # try to do so Python 2 will try to implicitly decode that byte string to
            # unicode using ascii first.
            #
            # This means that calling **encode()** can raise Unicode**Decode**Error!
            #
            # In Python 3 byte strings just don't have an encode() method.
            with pytest.raises(UnicodeDecodeError, match="^'ascii' codec can't decode byte"):
                utf8_byte_string.encode("utf-8")
    
    
    class TestReadingFromFiles(object):
    
        @python2
        def test_in_python_2_reading_text_from_file_returns_bytes_by_default(self):
            # Reading text from a file in "r" mode returns bytes in Python 2.
            text = open("hello.txt", "r").read()
    
            assert type(text) == bytes_type
            assert text == b"Hello world\n"
    
        @python3
        def test_in_python_3_reading_text_from_file_returns_unicode_by_default(self):
            # Reading text from a file in "r" mode returns unicode in Python 3.
            #
            # This decodes the bytes of the file using locale.getpreferredencoding()
            # (UTF-8 on Ubuntu).
            text = open("hello.txt", "r").read()
    
            assert type(text) == unicode_type
            assert text == u"Hello world\n"
    
        def test_you_can_read_bytes_from_file_too(self):
            text = open("hello.txt", "rb").read()
    
            assert type(text) == bytes_type
            assert text == b"Hello world\n"
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/

Manages JSON calls to S3DB web services:

URL for s3dbcall function: [http://s3dbcall.googlecode.com/hg/s3dbcall.js](http://s3dbcall.googlecode.com/hg/s3dbcall.js)

**Summary**

The s3dbcall function manages JSONP calls to a S3DB web services. Execution only requires that this URL is included in the SRC property of a SCRIPT DOM element.

See [http://www.youtube.com/watch?v=W8S6aVRE5vA](http://www.youtube.com/watch?v=W8S6aVRE5vA), [http://www.youtube.com/watch?v=LZOLNT3\_KbI](http://www.youtube.com/watch?v=LZOLNT3_KbI) for a demo.

**Usage documentation**

call\_id = s3dbcall(src,next\_eval,else\_eval,tout)
Makes a URL call to a S3DB deployment using JSON
Arguments:
call\_id is the call identifier, useful for debugging and
> tracking call results, see below.
> src is the url, typically the url of the deployment's
> S3QL service concatenated with the S3QL query.
> src can also be an object with the S3QL arguments as
> properties. The parameters url and key can also be passed
> as properties of the s3dlcall object (see examples).
> next\_eval is the command that is to be executed AFTER a
> sucessful call.
> else\_eval is the command that is to be executed if the
> call fails to respond.
> tout (timeout) is the time in milliseconds the call waits
> for a reply before deciding it failed. Note that
> if the reply arrives back after tout expires next\_eval
> will still be evaluated. default value is 10000 (10secs).

Debugging and other advanced tools

> the s3db call returns the call id (var call), i.e. id=s3dbcall(...
> s3dbcall.job keeps track of both successful and failed calls
> which can be checked with this reference. Successful calls answers
> will be stored in s3dbcall.job[id](id.md) untill of tout expires it. Note that
> If the call was succesfull s3dbcall.job[id](id.md) is deleted, seasing
> to be available for use by other functions. If the call was
> unsuccessfull within tout time interval than the failed url is stored
> with the sufix 'tout_', i.e. s3dbcall.job.tout\_call\_12345..._

> example 1:
> > `u='https://ibl.mdanderson.org/gcc/S3QL.php?y=abcdef&query=<S3QL><select>*</select><from>statements</from><where><rule_id>123</rule_idproject_id>456</project_id></where></S3QL>';`


> or any other S3DB service, such as u='https://ibl.mdanderson.org/URI.php'

> `s3dbcall(u,"result=ans;alert(':-)')","result=0;alert(':-(')")`

> example 2:

> `q={url:'http://ibl.mdanderson.org/gcc',key:'abcdef',select:'*',from:'statements',where:{rule_id:123,project_id:456}};s3dbcall(q,"result=ans;alert(':-)')","result=0;alert(':-(')")`}

> example 3:

> {{{s3dbcall.url='http://ibl.mdanderson.org/gcc'; // preset url
> s3dbcall.key='abcdef'; // preset key
> // and thereafter S3QL calls can be more simply made as, for example
> s3dbcall({select:'
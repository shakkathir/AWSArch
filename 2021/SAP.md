### SAP - 2021 

### SAP 2021 | whitepaper | [Load Balancer](https://d1.awsstatic.com/whitepapers/architecture-considerations-for-migrating-load-balancers-to-aws.pdf)
## IAM - 1 ( Non Federated)
## IAM - 2 ( Federated)
## Compute

## Networking
> #alb, #global_accelerator
* Alternatively, when using ALBs, the underlying IP addresses of the compute nodes
    supporting the ALB are subject to change, for example, in response to scaling events.
    *Because an ALB is not supported by a static compute node, or static group of compute
    nodes, it does not support direct integration with Elastic IP addresses. Static IP
    addresses can still be provided to consumers of ALB-based applications via AWS
    Global Accelerator, a service that provides fixed entry points to your application* 

## Storage 
> #ebs  
> Neal  Storage Section - Q3  2021-09-18 13:04:28  
* The volume should be configured with 1-TB as gp2 volumes provide *3 IOPS per GB, 3000 IOPS / TB* which will allow the full 3,000 IOPS to be achieved.  
* This HDD volume type supports a maximum of 500 IOPS per volume.  

>[aws link](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html)Between a minimum of 100 IOPS (at 33.33 GiB and below) and a maximum of 16,000 IOPS (at 5,334 GiB and above), baseline performance scales linearly at 3 IOPS per GiB of volume size. AWS designs gp2 volumes to deliver their provisioned performance 99% of the time. A gp2 volume can range in size from 1 GiB to 16 TiB.  
* EFS will be much more expensive than using a gp2 volume
___
> #s3 #s3-acls #s3-public-access  
> Neal Storage Section Q4 2021-09-18 15:10:56  
* [4 settings to block public access](https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-control-block-public-access.html#:~:text=settings-,s3%20block%20public%20access%20provides%20four%20settings,-.)
* [stackoverflow example for full understanding](https://stackoverflow.com/questions/64303953/what-does-these-settings-mean-for-block-public-access-settings-in-s3#:~:text=for%20example%2C%20aws%20s3%20api%20has%20a%20call%20such%20as%20put-object%20have%20option%20--acl.%20with%20this%20you%20can%20not%20only%20upload%20object%2C%20but%20also%20make%20it%20publicly)
* [S3 predefined groups](https://docs.aws.amazon.com/AmazonS3/latest/userguide/acl-overview.html#:~:text=amazon%20s3%20predefined%20groups)
* [canned acl](https://docs.aws.amazon.com/AmazonS3/latest/userguide/acl-overview.html#:~:text=amazon%20s3%20supports%20a%20set%20of%20predefined%20grants%2C)
<div class="votecell post-layout--left">
    <div class="js-voting-container d-flex jc-center fd-column ai-stretch gs4 fc-black-200" data-post-id="64304415">
        <div class="js-vote-count flex--item d-flex fd-column ai-center fc-black-500 fs-title" itemprop="upvoteCount" data-value="5"></div>
        <button class="js-vote-down-btn flex--item s-btn s-btn__unset c-pointer " data-controller="s-tooltip" data-s-tooltip-placement="right" aria-pressed="false" aria-label="Down vote" data-selected-classes="fc-theme-primary" data-unselected-classes="" aria-describedby="--stacks-s-tooltip-rnt59s5z">
            <svg aria-hidden="true" class="svg-icon iconArrowDownLg" width="36" height="36" viewBox="0 0 36 36">
                <path d="M2 10h32L18 26 2 10z"></path>
            </svg>
        </button>
        <div id="--stacks-s-tooltip-rnt59s5z" class="s-popover s-popover__tooltip pe-none" aria-hidden="true" role="tooltip">This answer is not useful<div class="s-popover--arrow"></div>
        </div>


        <div class="js-accepted-answer-indicator flex--item fc-green-500 py6 mtn8 d-none" data-s-tooltip-placement="right" title="Loading when this answer was accepted…" tabindex="0" role="note" aria-label="Accepted">
            <div class="ta-center">
                <svg aria-hidden="true" class="svg-icon iconCheckmarkLg" width="36" height="36" viewBox="0 0 36 36">
                    <path d="m6 14 8 8L30 6v8L14 30l-8-8v-8z"></path>
                </svg>
            </div>
        </div>


        <a class="js-post-issue flex--item s-btn s-btn__unset c-pointer py6 mx-auto" href="https://stackoverflow.com/posts/64304415/timeline" data-shortcut="T" data-ks-title="timeline" data-controller="s-tooltip" data-s-tooltip-placement="right" aria-label="Timeline" aria-describedby="--stacks-s-tooltip-f4ldl7t1"><svg aria-hidden="true" class="mln2 mr0 svg-icon iconHistory" width="19" height="18" viewBox="0 0 19 18">
                <path d="M3 9a8 8 0 113.73 6.77L8.2 14.3A6 6 0 105 9l3.01-.01-4 4-4-4h3L3 9zm7-4h1.01L11 9.36l3.22 2.1-.6.93L10 10V5z"></path>
            </svg></a>
        <div id="--stacks-s-tooltip-f4ldl7t1" class="s-popover s-popover__tooltip pe-none" aria-hidden="true" role="tooltip">Show activity on this post.<div class="s-popover--arrow"></div>
        </div>

    </div>

</div>



<div class="answercell post-layout--right">

    <div class="s-prose js-post-body" itemprop="text">
        <blockquote>
            <p>How does BlockPublicAcls and IgnorePublicAcls work differently?</p>
        </blockquote>
        <p><em class="diigoHighlight id_19c6e51b6c01d8436bb65cc18649068c type_0 yellow">For example, AWS S3 api has a call such as </em><a href="https://docs.aws.amazon.com/cli/latest/reference/s3api/put-object.html" rel="noreferrer"><em class="diigoHighlight id_19c6e51b6c01d8436bb65cc18649068c type_0 yellow">put-object</em></a><em class="diigoHighlight id_19c6e51b6c01d8436bb65cc18649068c type_0 yellow"> have option </em><code><em class="diigoHighlight id_19c6e51b6c01d8436bb65cc18649068c type_0 yellow">--acl</em></code><em class="diigoHighlight id_19c6e51b6c01d8436bb65cc18649068c type_0 yellow">. With this you can not only upload object, but also make it publicly available.<span class="diigoHighlightCommentLocator"></span></em></p>
        <div class="diigoIcon id_19c6e51b6c01d8436bb65cc18649068c type_9 TextIcon yellow" title="" style="bottom: 0px;"></div>
        <p></p>
        <p>When <code>Block Public Access</code> is off, call</p>
        <pre><code>a<em class="diigoHighlight id_6c31c52ed45a56bf928f8ba0fcc3ecd3 type_0 yellow">ws s3api put-object --bucket some-bucket --acl public-read --key test.file<span class="diigoHighlightCommentLocator"><div class="diigoIcon id_6c31c52ed45a56bf928f8ba0fcc3ecd3 type_9 TextIcon yellow" title="" style="bottom: 0px;"></div></span></em>
</code></pre>
        <p>successes, and <code>test.file</code> will be not only uploaded, but also publicly available.</p>
        <p>Now, if you enable:</p>
        <ul>
            <li><code>BlockPublicAcls</code>: the above <strong>API will fail</strong>. Any API which allows <code><em class="diigoHighlight id_49e6324089f66b83b2cbe61ab74e7cdc type_0 yellow">--acl public-read<span class="diigoHighlightCommentLocator">
                            <div class="diigoIcon id_49e6324089f66b83b2cbe61ab74e7cdc type_9 TextIcon yellow" title="" style="bottom: 0px;"></div>
                        </span></em></code> will be rejected. So <code>test.file</code> won't be uploaded.</li>
            <li><code>IgnorePublicAcls</code>: <strong>API call succeeds</strong>. The file is uploaded, but option <code><em class="diigoHighlight id_3a8e7f80a609b6a2c8260c0affbe431b type_0 yellow">--acl public-read<span class="diigoHighlightCommentLocator">
                            <div class="diigoIcon id_3a8e7f80a609b6a2c8260c0affbe431b type_9 TextIcon yellow" title="" style="bottom: 0px;"></div>
                        </span></em></code> is <strong>ignored</strong> and the file is private.</li>
        </ul>
        <blockquote>
            <p><em class="diigoHighlight id_75379062f542e2b2bc8514a024560926 type_0 yellow">How does BlockPublicPolicy and RestrictPublicBuckets work differently?</em></p>
        </blockquote>
    </div>
</div>
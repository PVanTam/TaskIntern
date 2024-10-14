# Information Gathering
>Tên tài liệu: Information Gathering<br>
Thực hiện: Phạm Văn Tam <br>
Cập nhật lần cuối: 14/10/2024
>
# Mục Lục
[1.Target ](#p1) <br>
[2. Conduct Search Engine Discovery Reconnaissance for Information Leakage](#p1) <br>
# Nội dung
<a id="p1"></a>
## 1. Target
Wildcard: `*.sqills.com`
<a id="p2"></a>
## 2. Tìm subdomain
```
subfinder -d sqills.com -o subfinder.txt

assetfinder --subs-only sqills.com | tee assetfinder.txt

findomain -t sqills.com -q | tee find-domain.txt

cat *.txt > all.txt && sort -u all.txt -o all.txt
```

Tìm thấy 864 subdomain
![image](https://github.com/user-attachments/assets/4f501614-73e7-402f-8800-f6e5a0d88c76)
<a id="p3"></a>
## 3. Check subdomain live
Bây giờ chúng ta đã có rất nhiều subdomains, nhưng biết rằng sẽ có nhiều subdomains không hoạt động. Chúng ta dùng httpx. <br>
```
cat all.txt | httpx -l all.txt -o live_domains.txt
```
Và kết quả :
```
https://api.autodandomain-controllererfig-www.test.sqills.com
https://api.brightline-prod.cloud.sqills.com
http://alt-booking.ouigo-acc.sqills.com
https://api.ouigo-acc.sqills.com
https://api.sqills-integration-dev-test.cloud.sqills.com
http://api.ouibus-prod.cloud.sqills.com
https://arriva-aap.mock.test.sqills.com
https://autodandomain-vendorersplunkig-lab-o1.test.sqills.com
https://backend-autodandomainshopdata.dashboard.prod.sqills.com
https://backend-autodandomainshopdata.prod.sqills.com
https://backoffice.irishrail-prod.cloud.sqills.com
http://autodandomain-vendorersplunkig-lab.test.sqills.com
http://backend-autodandomainshopdata-origin.prod.sqills.com
http://autodandomain-controllererfig-www.admin.test.sqills.com
http://autodandomain-controllererfig-www.test.sqills.com
http://backoffice.ouibus.prod.sqills.com
https://bom.irishrail-prod.cloud.sqills.com
https://booking-vanilla.ouigo-acc.sqills.com
https://bitbucket.sqills.com
https://booking.blablabus-acc.cloud.sqills.com
https://bom.irishrail-integration-test.cloud.sqills.com
https://bom.irishrail-dev-test.cloud.sqills.com
https://booking.irishrail-dev-test.cloud.sqills.com
https://booking.irishrail-prod.cloud.sqills.com
https://booking.irishrail-preprod-acc.cloud.sqills.com
http://booking.ouigo-preprod-acc.cloud.sqills.com
http://booking.ouigo-training-test.cloud.sqills.com
https://coreautodandomain-vendorerfig-lab.accept.sqills.com
https://cvs.test.sqills.com
https://booking2.ouigo-training-test.cloud.sqills.com
https://community.sqills.com
https://confluence.sqills.com
https://data.irishrail-integration-test.cloud.sqills.com
https://dev2-a.itabus-b-acc.cloud.sqills.com
https://client-autodandomain-vendorersplunkig-lab.test.sqills.com
https://booking2.ouigo-b-acc.cloud.sqills.com
https://dummy.ouibus-prod.cloud.sqills.com
https://data.irishrail-dev-test.cloud.sqills.com
https://ext-135.vdc.sqills.com
https://ext-138.vdc.sqills.com
https://ext-137.vdc.sqills.com
https://ext-143.vdc.sqills.com
https://d-cobs.prod.sqills.com
https://ext-155.vdc.sqills.com
https://ext-158.vdc.sqills.com
https://careers.sqills.com
https://data.irishrail-prod.cloud.sqills.com
http://ecobee.h-135-207-103-31.prod.sqills.com
https://jira-account-manager.cloud.sqills.com
https://maps.ouigo-acc.sqills.com
https://maps.trenitalia-test.cloud.sqills.com
http://k8s.autodandomain-vendorersplunkig-lab.test.sqills.com
https://ovidius-htm.accept.sqills.com
https://ouibus-booking.test.sqills.com
https://ouibus-backoffice.test.sqills.com
http://ovidius-gvb.prod.sqills.com
http://payment.ouigo-acc.sqills.com
http://ovidius-gvb.test.sqills.com
http://payment.sqills-infra-test.cloud.sqills.com
http://ovidius-htm.test.sqills.com
http://partner-testbeddandomaintrip.ouigo-acc.sqills.com
https://qbuzz.accept.sqills.com
https://s3-portal.sqills-integration-dev-test.cloud.sqills.com
https://s3a-backoffice.test.sqills.com
http://payment.trenitalia-test.cloud.sqills.com
https://s3-portal.ouigo-acc.sqills.com
https://s3p-care.ouigo-acc.sqills.com
https://s3p-cgi.ter-hno-prod.cloud.sqills.com
https://s3p-cgi.ter-hno-training-test.cloud.sqills.com
https://s3p-core.ouigo-acc.sqills.com
https://s3p-amplifier.ouigo-acc.sqills.com
https://pure-energie.prod.sqills.com
https://s3p-jenkins.ouigo-acc.sqills.com
https://s3p-cgi.ter-hno-dev-test.cloud.sqills.com
https://s3p-cgi.ter-hno-preprod-acc.cloud.sqills.com
http://s3p-jdarpo.ouigo-acc.sqills.com
https://s3p-sbsg.falbala-dev-test.cloud.sqills.com
https://s3passenger-backoffice.test.sqills.com
https://sqills.com
http://s3p-ssim.ouigo-acc.sqills.com
https://support.sqills.com
https://template.trenitalia-test.cloud.sqills.com
https://template.viarail-prod.cloud.sqills.com
https://ticket.brightline-prod.cloud.sqills.com
https://syntus.accept.sqills.com
https://ticket.ouigo-acc.sqills.com
https://ticket.irishrail-prod.cloud.sqills.com
https://syntus.test.sqills.com
https://ticket.ilsa-prod.cloud.sqills.com
https://ticket.ter-hno-prod.cloud.sqills.com
https://ticket.ouigoespana-prod.cloud.sqills.com
https://ticket.sj-prod.cloud.sqills.com
https://template.sj-integration-acc.cloud.sqills.com
https://ssim.ouigo-acc.sqills.com
https://webshop-htm.prod.sqills.com
https://v1-autodandomain-controllererfig-www.test.sqills.com
https://webshop-arriva.accept.sqills.com
https://statics.sqills.com
https://webshop-gvb.test.sqills.com
https://webshop-gvb.accept.sqills.com
https://webshop-qbuzz.prod.sqills.com
https://www.payment.ouigo-acc.sqills.com
http://ticket.viarail-prod.cloud.sqills.com
http://www.sqills.com
http://www.s3p-amplifier.ouigo-acc.sqills.com
http://www.s3p-ssim.ouigo-acc.sqills.com
http://www.s3p-cgi.ter-hno-prod.cloud.sqills.com
http://www.s3p-jdarpo.ouigo-acc.sqills.com
http://www.webshop-gvb.test.sqills.com
http://xbooker-s3accommodation.accept.sqills.com
http://www.upgrade-xbooker.accept.sqills.com
http://www.ssim.ouigo-acc.sqills.com
https://zakelijk-arriva.accept.sqills.com
http://www.ticket.ouigo-acc.sqills.com
http://www.webshop-htm.prod.sqills.com
http://zabbix.sqills.com
```
<a id="p4"></a>
## 4. Thu thập tất cả các URL và endpoint
waymore : <br>
```
waymore -i "sqills.com" -mode U -oU waymore.txt
```
![image](https://github.com/user-attachments/assets/34589bf5-29ed-44cd-a4f2-08cc68d89ce6) <br>
Kết quả :
```
http://booking.izy-dev-test.sqills.com/
https://careers.sqills.com/rust-developer-2/nl/apply
https://careers.sqills.com/international-business-consultant-5/en
https://www.sqills.com/knowledge-hub/s3-passenger-from-sqills-now-powers-swedish-rail-operator-sj
https://careers.sqills.com/business-application-specialist-4/nl/apply
https://booking.juniorcie-prod.cloud.sqills.com/ticket/VAL6JU_191015174728372.pdf
https://www.sqills.com/knowledge-hub
https://careers.sqills.com/software-tester
https://careers.sqills.com/software-tester-4
http://booking.sqills-infra-aws-test.sqills.com/
https://www.sqills.com/sqills-to-attend-world-passenger-festival
https://www.sqills.com/knowledge-hub/sqills-and-benerail-join-forces-to-further-implement-osdm-standardisation
https://careers.sqills.com/rust-developer-3
https://www.sqills.com/eurostar-now-live-on-s3-passenger/
https://www.sqills.com/event
https://www.sqills.com/knowledge-hub/eurostar-live-on-s3-passenger
https://www.sqills.com/cases/junior-cie/
https://careers.sqills.com/project-manager-2
https://sqills.com/knowledge-hub/open-access-and-reserved-two-public-transport-options-getting-closer
https://careers.sqills.com/business-application-specialist-4/nl
https://booking.shared.ouigo-acc.cloud.sqills.com/
https://careers.sqills.com/international-business-consultant-5
https://careers.sqills.com/robots.txt
https://www.sqills.com/cases/ouigo
http://www.sqills.com/en/
https://www.sqills.com/
https://careers.sqills.com/information-security-privacy-officer
https://www.sqills.com/sqills-is-now-pci-dss-level-1-certified
https://careers.sqills.com/product-owner-information-analyst/en
http://msa-shared.sqills.com/
https://careers.sqills.com/performance-engineer/en
https://www.sqills.com/social-distancing-in-public-transport/
https://www.sqills.com/knowledge-hub/sqills-expands-its-european-coverage-with-s3-passenger-for-ouigo-spain
https://careers.sqills.com/product-owner-information-analyst
https://www.sqills.com/cases/irish-rail
https://www.sqills.com/knowledge-hub/sqills-at-innotrans-2022-in-berlin
https://careers.sqills.com/rust-developer-2/en/apply
https://careers.sqills.com/
https://careers.sqills.com/trainee-business-application-specialist
https://booking.izy-acc.cloud.sqills.com/
https://www.sqills.com/knowledge-hub/sqills-to-provide-osdm-validator-tool-to-the-international-rail-it-community-to-enhance-standardisation
https://careers.sqills.com/software-developer-eldorado
http://sqills.com/
https://sqills.com/robots.txt
https://www.sqills.com/cases/eurostar
https://careers.sqills.com/talent-acquisition-specialist/en/apply
http://www.sqills.com/robots.txt
https://ticket.juniorcie-prod.cloud.sqills.com/ticket/8R6BKG_240326092723005.pdf
https://www.sqills.com/technical-blogs/insecure-deserialization
https://www.sqills.com/innotrans-2022-in-berlin
https://www.sqills.com/knowledge-hub/iarnrod-eireann-irish-rail-extends-s3-passenger-contract-into-saas-mode
https://www.sqills.com/event/
https://www.sqills.com/knowledge-hub/iryo-12-month-implementation
https://www.sqills.com/nl/event/
https://www.sqills.com/nl/event
https://www.sqills.com/knowledge-hub/sqills-to-join-siemens-mobility
https://careers.sqills.com/software-tester/en
https://careers.sqills.com/performance-engineer/en/apply
https://www.sqills.com/cases/blablabus
https://www.sqills.com/knowledge-hub/irish-rail-s3-passenger-environment-now-migrated-to-aws-cloud
https://careers.sqills.com/junior-software-tester-2
https://www.sqills.com/cases/snaelltaget
https://www.sqills.com/knowledge-hub/sqills-powers-itabus
https://careers.sqills.com/software-developer/en/apply
https://www.sqills.com/contact
https://careers.sqills.com/business-consultancy-traineeship
https://careers.sqills.com/international-business-consultant-6
https://careers.sqills.com/software-tester/en/apply
https://careers.sqills.com/financial-bid-manager
https://www.sqills.com/knowledge-hub/commercial-seat-selection-features-in-s3-passenger
http://booking.eurostar-integration-test.sqills.com/
https://careers.sqills.com/project-manager-2/en
https://www.sqills.com/eurostar-now-live-on-s3-passenger
https://www.sqills.com/cases/hkx
https://careers.sqills.com/software-developer-2
http://confluence.sqills.com/
https://www.sqills.com/knowledge-hub/open-access-and-reserved-two-public-transport-options-getting-closer
https://www.sqills.com/innotrans-2022-in-berlin/
https://careers.sqills.com/business-application-specialist-4/en/apply
https://www.sqills.com/knowledge-hub/sncf-selects-s3-passenger-as-their-new-reservation-system
https://www.sqills.com/knowledge-hub/swedish-rail-operator-sj-to-strengthen-its-digital-capabilities
https://www.sqills.com/cases/ter
https://confluence.sqills.com/display/KNOW/Sqillguard
https://careers.sqills.com/software-tester-4/en/apply
https://booking.worldpay-mock.ouigo-preprod-acc.cloud.sqills.com/
https://www.sqills.com/contact/
https://www.sqills.com/technical-blogs/insecure-deserialization/
https://www.sqills.com/knowledge-hub/osdm-and-sqills-what-it-means-now-and-going-forward
https://www.sqills.com/?gclid=Cj0KCQjwtO-kBhDIARIsAL6LorfDCwqdVdlAmVhf2NXyDV4LFjad57Qqr_yWgPyBbPnSUMvimXL_QHYaAnzyEALw_wcB
https://careers.sqills.com/rust-developer-3/nl
https://careers.sqills.com/business-application-specialist-3/en
https://www.sqills.com/en/
https://www.sqills.com/knowledge-hub/snaelltaget-selects-s3-passenger-to-power-its-business
https://careers.sqills.com/international-business-consultant-5/en/apply
https://www.sqills.com/cases/junior-cie
http://cloud.sqills.com/
https://k8s-prdbooking.ouigo-preprod-acc.cloud.sqills.com/
https://www.sqills.com/cases
https://www.sqills.com/technical-blogs/s3-load-testing/
https://careers.sqills.com/?lang=en
https://www.sqills.com/knowledge-hub/new-partnership-with-ter-sqills-gains-more-foothold-in-france
https://www.sqills.com/robots.txt
https://www.sqills.com/sqills-now-powers-italian-bus-startup-itabus
https://www.sqills.com/sqills-now-powers-italian-bus-startup-itabus/
https://careers.sqills.com/software-developer
https://www.sqills.com/first-british-carriers-now-live-on-s3-passenger
https://www.sqills.com/nl/jobs/trainee-customer-support-engineer/
https://careers.sqills.com/rust-developer-2
https://www.sqills.com/social-distancing-in-public-transport
https://www.sqills.com/technical-blogs/managing-threats-by-monitoring-the-public-internet/
https://careers.sqills.com/talent-acquisition-specialist
https://careers.sqills.com/software-developer-2/en
https://www.sqills.com/s3-passenger
https://careers.sqills.com/rust-developer-3/nl/apply
https://www.sqills.com/knowledge-hub/sqills-to-attend-the-smart-city-summit-expo-in-taiwan
https://www.sqills.com/knowledge-hub/first-british-carriers-now-live-on-s3-passenger
https://www.sqills.com/cases/itabus
https://www.sqills.com/knowledge-hub/sqills-working-with-the-rdg-to-transform-rail-travel-across-the-uk-network
https://careers.sqills.com/rust-developer-2/nl
https://ticket.irishrail-prod.cloud.sqills.com/ticket/61846628_240920124943959.pdf
https://www.sqills.com/implementation
http://booking.izy-acc.cloud.sqills.com/
https://careers.sqills.com/business-application-specialist-3
https://www.sqills.com/knowledge-hub/brightline-to-implement-state-of-the-art-inventory-and-reservation-system
https://api.ouibus-prod.cloud.sqills.com/
https://www.sqills.com/en/cases/arriva/arriva-website-and-app
https://careers.sqills.com/business-application-specialist-4/en
https://www.sqills.com/nl/sollicitatieprocedure/
https://careers.sqills.com/project-manager-2/en/apply
https://www.sqills.com/knowledge-hub/go-live-with-benerail-a-fact-after-10-month-implementation-period
https://careers.sqills.com/business-application-specialist-4
https://www.sqills.com/nl/jobs/trainee-customer-support-engineer
http://ouigo-prod.cloud.sqills.com/
http://booking.eurostar-demo-test.sqills.com/
https://careers.sqills.com/international-business-consultant-6/en/apply
https://sqills.com/cases/itabus
http://booking.izy-acc.cloud.sqills.com:443/
https://careers.sqills.com/information-security-privacy-officer/en/apply
http://www.sqills.com/
https://www.sqills.com/knowledge-hub/sqills-is-now-pci-dss-level-1-certified
https://careers.sqills.com/junior-software-tester-2/en/apply
http://booking.oce-acc.sqills.com
http://booking.juniorcie-prod.cloud.sqills.com/
https://guard.sqills.com
https://careers.sqills.com/rust-developer-3/en/apply
https://www.sqills.com/sqills-to-attend-world-passenger-festival/
https://s3-portal.sqills-integration-dev-test.cloud.sqills.com/en-GB/portal
http://booking.sqills-infra-aws-test-saas.cloud.sqills.com/
https://careers.sqills.com/international-business-consultant-6/en
http://booking.sqills-dev-x-dev-test.sqills.com/
https://careers.sqills.com/software-developer-2/en/apply
https://careers.sqills.com/business-consultancy-traineeship/en/apply
http://booking.ouibus-b-acc.sqills.com/
https://careers.sqills.com/software-tester-4/en
https://careers.sqills.com/trainee-business-application-specialist/en
https://careers.sqills.com/experienced-software-developer-team-coach
https://careers.sqills.com/product-owner-information-analyst/en/apply
https://www.sqills.com/cases/izy
https://careers.sqills.com/information-security-privacy-officer/en
https://ticket.ilsa-prod.cloud.sqills.com/
https://www.sqills.com/technical-blogs/s3-load-testing
http://www.booking.izy-acc.cloud.sqills.com:443/
https://www.sqills.com/knowledge-hub/the-power-of-dynamic-pricing-with-s3-passenger-an-introduction
```
katana : <br>
```
cat live_domains.txt | katana -f qurl -silent -kf all -jc -aff -d 5 -o katana-param.txt
```
![image](https://github.com/user-attachments/assets/4db4d026-1925-4cba-b149-5be9bf205056)

<a id="p5"></a>
## 5. Check  các tệp sao lưu, tệp JavaScript, tệp PHP và nhiều loại tệp khác.
```
grep -E -i -o '\S+\.(cobak|backup|swp|old|db|sql|asp|aspx|aspx~|asp~|py|py~|rb|rb~|php|php~|bak|bkp|cache|cgi|conf|csv|html|inc|jar|js|json|jsp|jsp~|lock|log|r(ar|)\.old|sql|sql\.gz|sql\.zip|sql\.tar\.gz|sql~|swp|swp~|tar|tar\.bz2|tar\.gz|txt|wadl|zip|log|xml|json)\b' "waymore.txt" "katana-param.txt" | sort -u > interesting.txt
```
Kết quả: <br>
```
katana-param.txt:https://booking.irishrail-dev-test.cloud.sqills.com/js/app.1fb2870.js
katana-param.txt:https://booking.irishrail-dev-test.cloud.sqills.com/js/c.1fb2870.js
katana-param.txt:https://booking.irishrail-dev-test.cloud.sqills.com/js/format.1fb2870.js
katana-param.txt:https://booking.irishrail-dev-test.cloud.sqills.com/js/styles.1fb2870.js
katana-param.txt:https://booking.irishrail-dev-test.cloud.sqills.com/js/vendor.1fb2870.js
katana-param.txt:https://booking.irishrail-preprod-acc.cloud.sqills.com/js/app.1e86682.js
katana-param.txt:https://booking.irishrail-preprod-acc.cloud.sqills.com/js/c.1e86682.js
katana-param.txt:https://booking.irishrail-preprod-acc.cloud.sqills.com/js/format.1e86682.js
katana-param.txt:https://booking.irishrail-preprod-acc.cloud.sqills.com/js/styles.1e86682.js
katana-param.txt:https://booking.irishrail-preprod-acc.cloud.sqills.com/js/vendor.1e86682.js
katana-param.txt:https://community.sqills.com/theme-javascripts/0030e5af30a2d12177ba27f3e4b6fb9e7c214ba1.js
katana-param.txt:https://community.sqills.com/theme-javascripts/34210dc62c52908987af12712e441bb9962079d1.js
katana-param.txt:https://community.sqills.com/theme-javascripts/463db91f28b90cdc4d6dac6f2fb7637855b30f1b.js
katana-param.txt:https://community.sqills.com/theme-javascripts/6d08db7d815462205edf1fd0012ec39375921944.js
katana-param.txt:https://community.sqills.com/theme-javascripts/861e5faeecbc381511f72056f4b25cb1c00ce9e2.js
katana-param.txt:https://community.sqills.com/theme-javascripts/97a6b518c692dd408de54233bb6e99c9dc79ef4e.js
katana-param.txt:https://community.sqills.com/theme-javascripts/a6c08106d26fcf146bf72285968a7c55338bd9fa.js
katana-param.txt:https://community.sqills.com/theme-javascripts/a9199884e0e67609f710aac132d12807e9965683.js
katana-param.txt:https://community.sqills.com/theme-javascripts/bb1db306ebb4eff5e620006cedb11adff1586c13.js
katana-param.txt:https://community.sqills.com/theme-javascripts/bd887dd83c6a5050f52c8bac59baaf2881dc60bb.js
katana-param.txt:https://community.sqills.com/theme-javascripts/ced7e6b279eb3ea2b7de61be31f44ab3641f795a.js
katana-param.txt:https://community.sqills.com/theme-javascripts/d5df25e9f4db3ea1c87af730b66c0fa4cbc19285.js
katana-param.txt:https://community.sqills.com/theme-javascripts/dbfb9a1ed67e22b5a187738f1d9967d50c5683ba.js
katana-param.txt:https://community.sqills.com/theme-javascripts/eeabafc48955a53d8091600fa787d1ef0dd2036c.js
katana-param.txt:https://community.sqills.com/theme-javascripts/fa40cf1a787564d63cb44bc95f49c0cbecd12a1e.js
katana-param.txt:https://community.sqills.com/timings.json
katana-param.txt:https://community.sqills.com/user_actions.json
katana-param.txt:https://confluence.sqills.com/login.action?os_destination=https%3A%2F%2Fconfluence.sqills.com%2FS3PDOC%2Ffunctional-documentation-46352781.html
katana-param.txt:https://confluence.sqills.com/login.action?os_destination=https%3A%2F%2Fconfluence.sqills.com%2FS3PDOC%2Frelease-notes-46364330.html
katana-param.txt:https://confluence.sqills.com/login.action?os_destination=https%3A%2F%2Fconfluence.sqills.com%2FS3PDOC%2Froadmap-50907793.html
katana-param.txt:https://confluence.sqills.com/login.action?os_destination=https%3A%2F%2Fconfluence.sqills.com%2FS3PDOC%2Ftechnical-documentation-46364858.html
katana-param.txt:https://confluence.sqills.com/login.action?os_destination=https%3A%2F%2Fconfluence.sqills.com%2FS3PDOC%2Ftraining-88330046.html
katana-param.txt:https://confluence.sqills.com/s/33c9c38a36e93ec66fae13982fee5e1a-T/-bn9hrx/9104/1nd5f50/b622c6ca68e961915b7c0bc5a59390bc/_/download/contextbatch/js/main,atl.general,-_super/batch.js
katana-param.txt:https://confluence.sqills.com/s/50f684a9948364ce81c76cd604f89440-CDN/-bn9hrx/9104/1nd5f50/eb4784fc3dbb7130b0b09f6fb9679fc4/_/download/contextbatch/js/_super,-com.atlassian.plugins.atlassian-plugins-webresource-rest:data-collector-perf-observer/batch.js
katana-param.txt:https://confluence.sqills.com/s/ca22ff1e702803f29e667febbaa2bb5a-CDN/-bn9hrx/9104/1nd5f50/4.3.11/_/download/batch/com.atlassian.plugins.authentication.atlassian-authentication-plugin:entrypoint-login-page-ui/com.atlassian.plugins.authentication.atlassian-authentication-plugin:entrypoint-login-page-ui.js
katana-param.txt:https://support.sqills.com/login.jsp
katana-param.txt:https://support.sqills.com/login.jsp?os_destination=%2Flogin.jsp
katana-param.txt:https://support.sqills.com/login.jsp?os_destination=https%3A%2F%2Fsupport.sqills.com%2Fsecure%2Fresource-phase-checkpoint-init%2Fbatch.js
katana-param.txt:https://support.sqills.com/login.jsp?os_destination=https%3A%2F%2Fsupport.sqills.com%2Fsecure%2F-_super%2Fbatch.js
katana-param.txt:https://support.sqills.com/login.jsp?os_destination=https%3A%2F%2Fsupport.sqills.com%2Fu0022%2Flogin.jsp
katana-param.txt:https://support.sqills.com/login.jsp?os_destination=https%3A%2F%2Fsupport.sqills.com%2Fu0022%2Fsecure%2FConfigureReport.jsp
katana-param.txt:https://support.sqills.com/login.jsp?os_destination=https%3A%2F%2Fsupport.sqills.com%2Fu0022%2Fsecure%2FViewProfile.jsp
katana-param.txt:https://support.sqills.com/s/06bbcda412281f81389a0863e5c85d70-CDN/-k9b11j/9150002/1p2gz7g/4.3.10/_/download/batch/com.atlassian.plugins.authentication.atlassian-authentication-plugin:entrypoint-login-page-ui/com.atlassian.plugins.authentication.atlassian-authentication-plugin:entrypoint-login-page-ui.js
waymore.txt:https://careers.sqills.com/robots.txt
waymore.txt:https://sqills.com/robots.txt
waymore.txt:https://www.sqills.com/robots.txt
waymore.txt:http://www.sqills.com/robots.txt
```
Tiến hành loại bỏ tất cả các URL trùng lặp và các tệp có phần mở rộng không cần thiết như jpeg, png, icon, v.v. <br>
```
cat waymore.txt katana-param.txt | sort -u | grep "=" | qsreplace 'FUZZ' | egrep -v '(.css|.png|blog|utm_source|utm_content|utm_campaign|utm_medium|.jpeg|.jpg|.svg|.gifs|.tif|.tiff|.png|.ttf|.woff|.woff2|.ico|.pdf|.svg|.txt|.gif|.wolf)' > waymore-katana-unfilter-urls.txt
```
Kết quả : <br>
```
https://booking.ouigo-training-test.cloud.sqills.com:443/user-account/deep-link/finalization?e=FUZZ
https://careers.sqills.com/?lang=FUZZ
https://community.sqills.com/admin/customize/site_texts?q=FUZZ
https://community.sqills.com/admin/site_settings/category/all_results?filter=FUZZ
https://community.sqills.com/extra-locales/mf?v=FUZZ
https://community.sqills.com/l/latest?assigned=FUZZ&status=FUZZ
https://community.sqills.com/search?q=FUZZ
https://community.sqills.com/session/sso?return_path=FUZZ
https://community.sqills.com/theme-javascripts/0030e5af30a2d12177ba27f3e4b6fb9e7c214ba1.js?__ws=FUZZ
https://community.sqills.com/theme-javascripts/34210dc62c52908987af12712e441bb9962079d1.js?__ws=FUZZ
https://community.sqills.com/theme-javascripts/463db91f28b90cdc4d6dac6f2fb7637855b30f1b.js?__ws=FUZZ
https://community.sqills.com/theme-javascripts/6d08db7d815462205edf1fd0012ec39375921944.js?__ws=FUZZ
https://community.sqills.com/theme-javascripts/861e5faeecbc381511f72056f4b25cb1c00ce9e2.js?__ws=FUZZ
https://community.sqills.com/theme-javascripts/97a6b518c692dd408de54233bb6e99c9dc79ef4e.js?__ws=FUZZ
https://community.sqills.com/theme-javascripts/a6c08106d26fcf146bf72285968a7c55338bd9fa.js?__ws=FUZZ
https://community.sqills.com/theme-javascripts/a9199884e0e67609f710aac132d12807e9965683.js?__ws=FUZZ
https://community.sqills.com/theme-javascripts/bb1db306ebb4eff5e620006cedb11adff1586c13.js?__ws=FUZZ
https://community.sqills.com/theme-javascripts/bd887dd83c6a5050f52c8bac59baaf2881dc60bb.js?__ws=FUZZ
https://community.sqills.com/theme-javascripts/ced7e6b279eb3ea2b7de61be31f44ab3641f795a.js?__ws=FUZZ
https://community.sqills.com/theme-javascripts/d5df25e9f4db3ea1c87af730b66c0fa4cbc19285.js?__ws=FUZZ
https://community.sqills.com/theme-javascripts/dbfb9a1ed67e22b5a187738f1d9967d50c5683ba.js?__ws=FUZZ
https://community.sqills.com/theme-javascripts/eeabafc48955a53d8091600fa787d1ef0dd2036c.js?__ws=FUZZ
https://community.sqills.com/theme-javascripts/fa40cf1a787564d63cb44bc95f49c0cbecd12a1e.js?__ws=FUZZ
https://community.sqills.com/timings.json?last=FUZZ
https://community.sqills.com/user_actions.json
https://confluence.sqills.com/download/attachments/425986/atl.site.logo?api=FUZZ&modificationDate=FUZZ&version=FUZZ
https://confluence.sqills.com/login.action?os_destination=FUZZ&permissionViolation=FUZZ
https://confluence.sqills.com/s/33c9c38a36e93ec66fae13982fee5e1a-T/-bn9hrx/9104/1nd5f50/b622c6ca68e961915b7c0bc5a59390bc/_/download/contextbatch/js/main,atl.general,-_super/batch.js?hostenabled=FUZZ&locale=FUZZ&slack-enabled=FUZZ
https://confluence.sqills.com/s/50f684a9948364ce81c76cd604f89440-CDN/-bn9hrx/9104/1nd5f50/eb4784fc3dbb7130b0b09f6fb9679fc4/_/download/contextbatch/js/_super,-com.atlassian.plugins.atlassian-plugins-webresource-rest:data-collector-perf-observer/batch.js?locale=FUZZ
https://confluence.sqills.com/s/ca22ff1e702803f29e667febbaa2bb5a-CDN/-bn9hrx/9104/1nd5f50/4.3.11/_/download/batch/com.atlassian.plugins.authentication.atlassian-authentication-plugin:entrypoint-login-page-ui/com.atlassian.plugins.authentication.atlassian-authentication-plugin:entrypoint-login-page-ui.js?locale=FUZZ
https://support.sqills.com/login.jsp?jira.request.concurrent.requests=FUZZ
https://support.sqills.com/login.jsp?os_destination=FUZZ
https://support.sqills.com/login.jsp?jira.request.concurrent.requests=FUZZ&os_destination=FUZZ
https://support.sqills.com/login.jsp?os_destination=FUZZ&page_caps=FUZZ&permissionViolation=FUZZ&user_role=FUZZ
https://support.sqills.com/login.jsp?jira.request.concurrent.requests=FUZZ&os_destination=FUZZ&page_caps=FUZZ&permissionViolation=FUZZ&user_role=FUZZ
https://support.sqills.com/s/06bbcda412281f81389a0863e5c85d70-CDN/-k9b11j/9150002/1p2gz7g/4.3.10/_/download/batch/com.atlassian.plugins.authentication.atlassian-authentication-plugin:entrypoint-login-page-ui/com.atlassian.plugins.authentication.atlassian-authentication-plugin:entrypoint-login-page-ui.js?locale=FUZZ
https://support.sqills.com/secure/ConfigureReport!default.jspa?jira.request.concurrent.requests=FUZZ
https://support.sqills.com/secure/ConfigureReport.jspa?jira.request.concurrent.requests=FUZZ
https://support.sqills.com/secure/JiraCreditsPage!default.jspa?jira.request.concurrent.requests=FUZZ
https://www.sqills.com/?gclid=FUZZ
https://www.sqills.com/_next?%3F=FUZZ
https://www.sqills.com/_next?I=FUZZ
https://www.sqills.com/_next/image?q=FUZZ&url=FUZZ&w=FUZZ
https://www.sqills.com/_next?p=FUZZ
https://www.sqills.com/_next?XjC=FUZZ
```
<a id="p6"></a>
## 6. Tiến hành lọc lại cái endpoint
```
cat waymore-katana-unfilter-urls.txt | httpx -t 150 -rl 150 -o waymore-katana-filter-urls.txt
```
Bây giờ, lấy tất cả các URL từ danh sách đã lọc có chứa dấu =. Vì các URL này có thể được kiểm tra cho các lỗ hổng khác nhau như SQLi, LFI, XSS, và nhiều loại khác. <br>
```
grep = waymore-katana-filter-urls.txt >> parameters_with_equal.txt
```
Kết quả: <br>
```
https://www.sqills.com/_next?p=FUZZ
https://www.sqills.com/_next?%3F=FUZZ
https://www.sqills.com/?gclid=FUZZ
https://www.sqills.com/_next/image?q=FUZZ&url=FUZZ&w=FUZZ
https://www.sqills.com/_next?I=FUZZ
https://community.sqills.com/theme-javascripts/0030e5af30a2d12177ba27f3e4b6fb9e7c214ba1.js?__ws=FUZZ
https://community.sqills.com/timings.json?last=FUZZ
https://community.sqills.com/admin/site_settings/category/all_results?filter=FUZZ
https://community.sqills.com/extra-locales/mf?v=FUZZ
https://community.sqills.com/theme-javascripts/a6c08106d26fcf146bf72285968a7c55338bd9fa.js?__ws=FUZZ
https://community.sqills.com/search?q=FUZZ
https://community.sqills.com/theme-javascripts/fa40cf1a787564d63cb44bc95f49c0cbecd12a1e.js?__ws=FUZZ
https://community.sqills.com/theme-javascripts/463db91f28b90cdc4d6dac6f2fb7637855b30f1b.js?__ws=FUZZ
https://community.sqills.com/theme-javascripts/d5df25e9f4db3ea1c87af730b66c0fa4cbc19285.js?__ws=FUZZ
https://community.sqills.com/theme-javascripts/dbfb9a1ed67e22b5a187738f1d9967d50c5683ba.js?__ws=FUZZ
https://community.sqills.com/theme-javascripts/ced7e6b279eb3ea2b7de61be31f44ab3641f795a.js?__ws=FUZZ
https://community.sqills.com/theme-javascripts/bb1db306ebb4eff5e620006cedb11adff1586c13.js?__ws=FUZZ
https://community.sqills.com/admin/customize/site_texts?q=FUZZ
https://community.sqills.com/theme-javascripts/eeabafc48955a53d8091600fa787d1ef0dd2036c.js?__ws=FUZZ
https://community.sqills.com/theme-javascripts/a9199884e0e67609f710aac132d12807e9965683.js?__ws=FUZZ
https://community.sqills.com/theme-javascripts/bd887dd83c6a5050f52c8bac59baaf2881dc60bb.js?__ws=FUZZ
https://community.sqills.com/theme-javascripts/34210dc62c52908987af12712e441bb9962079d1.js?__ws=FUZZ
https://community.sqills.com/theme-javascripts/6d08db7d815462205edf1fd0012ec39375921944.js?__ws=FUZZ
https://booking.ouigo-training-test.cloud.sqills.com/user-account/deep-link/finalization?e=FUZZ
https://community.sqills.com/l/latest?assigned=FUZZ&status=FUZZ
https://community.sqills.com/theme-javascripts/861e5faeecbc381511f72056f4b25cb1c00ce9e2.js?__ws=FUZZ
https://community.sqills.com/session/sso?return_path=FUZZ
https://community.sqills.com/theme-javascripts/97a6b518c692dd408de54233bb6e99c9dc79ef4e.js?__ws=FUZZ
https://support.sqills.com/secure/ConfigureReport.jspa?jira.request.concurrent.requests=FUZZ
https://support.sqills.com/login.jsp?jira.request.concurrent.requests=FUZZ
https://support.sqills.com/login.jsp?os_destination=FUZZ&page_caps=FUZZ&permissionViolation=FUZZ&user_role=FUZZ
https://support.sqills.com/login.jsp?jira.request.concurrent.requests=FUZZ&os_destination=FUZZ
https://support.sqills.com/secure/ConfigureReport!default.jspa?jira.request.concurrent.requests=FUZZ
https://confluence.sqills.com/login.action?os_destination=FUZZ&permissionViolation=FUZZ
https://support.sqills.com/login.jsp?os_destination=FUZZ
https://support.sqills.com/login.jsp?jira.request.concurrent.requests=FUZZ&os_destination=FUZZ&page_caps=FUZZ&permissionViolation=FUZZ&user_role=FUZZ
https://www.sqills.com/_next?XjC=FUZZ
https://careers.sqills.com/?lang=FUZZ
https://confluence.sqills.com/download/attachments/425986/atl.site.logo?api=FUZZ&modificationDate=FUZZ&version=FUZZ
https://support.sqills.com/s/06bbcda412281f81389a0863e5c85d70-CDN/-k9b11j/9150002/1p2gz7g/4.3.10/_/download/batch/com.atlassian.plugins.authentication.atlassian-authentication-plugin:entrypoint-login-page-ui/com.atlassian.plugins.authentication.atlassian-authentication-plugin:entrypoint-login-page-ui.js?locale=FUZZ
https://support.sqills.com/secure/JiraCreditsPage!default.jspa?jira.request.concurrent.requests=FUZZ
https://confluence.sqills.com/s/ca22ff1e702803f29e667febbaa2bb5a-CDN/-bn9hrx/9104/1nd5f50/4.3.11/_/download/batch/com.atlassian.plugins.authentication.atlassian-authentication-plugin:entrypoint-login-page-ui/com.atlassian.plugins.authentication.atlassian-authentication-plugin:entrypoint-login-page-ui.js?locale=FUZZ
https://confluence.sqills.com/s/50f684a9948364ce81c76cd604f89440-CDN/-bn9hrx/9104/1nd5f50/eb4784fc3dbb7130b0b09f6fb9679fc4/_/download/contextbatch/js/_super,-com.atlassian.plugins.atlassian-plugins-webresource-rest:data-collector-perf-observer/batch.js?locale=FUZZ
https://confluence.sqills.com/s/33c9c38a36e93ec66fae13982fee5e1a-T/-bn9hrx/9104/1nd5f50/b622c6ca68e961915b7c0bc5a59390bc/_/download/contextbatch/js/main,atl.general,-_super/batch.js?hostenabled=FUZZ&locale=FUZZ&slack-enabled=FUZZ
```
<a id="p7"></a>
## 5. Check với Nuclei và Burp
Nuclei : <br>
```
nuclei -l parameters_with_equal.txt
```
![image](https://github.com/user-attachments/assets/cddf082c-4039-4e9c-9c53-f25ee8b0f6f1)












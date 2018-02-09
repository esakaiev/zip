Justification

Adds tests according to the CI wiki specifically the standard test interface in the spec.

The playbook includes Tier1 level test cases that have been tested in the following contexts and is passing reliably: Classic. Test logs are stored in the artifacts directory.

The following steps are used to execute the tests using the standard test interface:




Make sure you have installed packages from the spec

# sudo rpm -q ansible python2-dnf libselinux-python standard-test-roles \
ansible-2.3.2.0-1.fc26.noarch \
python2-dnf-2.6.3-11.fc26.noarch \
libselinux-python-2.6-7.fc26.x86_64 \
standard-test-roles-2.4-1.fc26.noarch

sudo yum install zip

Run tests for Classic
# export ANSIBLE_INVENTORY=$(test -e inventory && echo inventory || echo /usr/share/ansible/inventory)
# ansible-playbook --tags=classic tests.yml

Snip of the example test run for Classic tests:

TASK [standard-test-behave : Check the results] *******************************************************************************************************************************************************************
changed: [localhost]

PLAY RECAP ********************************************************************************************************************************************************************************************************
localhost                  : ok=7   changed=1    unreachable=0    failed=0   

PASS test_4GBsegfault
PASS test_big_file_in_archive
PASS test_long_path_in_archive
PASS test_many_files_in_archive
PASS test_umask
PASS test_umask_when_creating
PASS test_zipnote_fails_to_update_the_archive

Notes

Tests will be enabled in CI, yet gating is currently disabled, so nothing will change. Tests will run on each dist-git commit, they are not triggered on koji builds and if you are using FMN, it should notify you of failures normally.

The RH QE maintainer contact in case you have questions: esakaiev @redhat.com
The idea is that these tests become yours just as you're maintaining the package, there will, of course, be people around if you have questions or troubles.

Tests have been tested under Fedora_27 and Rawhide_(February 04, 2018).
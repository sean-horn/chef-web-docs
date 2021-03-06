---
resource_reference: true
resources_common_guards: true
resources_common_notification: true
resources_common_properties: true
title: openssl_rsa_public_key resource
resource: openssl_rsa_public_key
aliases:
- "/resource_openssl_rsa_public_key.html"
menu:
  infra:
    title: openssl_rsa_public_key
    identifier: chef_infra/cookbook_reference/resources/openssl_rsa_public_key openssl_rsa_public_key
    parent: chef_infra/cookbook_reference/resources
resource_description_list:
- markdown: Use the **openssl_rsa_public_key** resource to generate RSA public key
    files for a given RSA private key.
resource_new_in: '14.0'
syntax_full_code_block: |-
  openssl_rsa_public_key 'name' do
    group                    String, Integer
    mode                     Integer, String # default value: "0640"
    owner                    String, Integer
    path                     String # default value: 'name' unless specified
    private_key_content      String
    private_key_pass         String
    private_key_path         String
    action                   Symbol # defaults to :create if not specified
  end
syntax_properties_list:
syntax_full_properties_list:
- "`openssl_rsa_public_key` is the resource."
- "`name` is the name given to the resource block."
- "`action` identifies which steps Chef Infra Client will take to bring the node into
  the desired state."
- "`group`, `mode`, `owner`, `path`, `private_key_content`, `private_key_pass`, and
  `private_key_path` are the properties available to this resource."
actions_list:
  :create:
    markdown: Default. Create the RSA public key.
  :nothing:
    shortcode: resources_common_actions_nothing.md
properties_list:
- property: group
  ruby_type: String, Integer
  required: false
  description_list:
  - markdown: The group ownership applied to all files created by the resource.
- property: mode
  ruby_type: Integer, String
  required: false
  default_value: '0640'
  description_list:
  - markdown: The permission mode applied to all files created by the resource.
- property: owner
  ruby_type: String, Integer
  required: false
  description_list:
  - markdown: The owner applied to all files created by the resource.
- property: path
  ruby_type: String
  required: false
  default_value: The resource block's name
  description_list:
  - markdown: An optional property for specifying the path to the public key if it
      differs from the resource block's name.
- property: private_key_content
  ruby_type: String
  required: false
  description_list:
  - markdown: The content of the private key, including new lines. This property is
      used in place of private_key_path in instances where you want to avoid having
      to first write the private key to disk.
- property: private_key_pass
  ruby_type: String
  required: false
  description_list:
  - markdown: The passphrase of the provided private key.
- property: private_key_path
  ruby_type: String
  required: false
  description_list:
  - markdown: The path to the private key file.
examples: |
  Generate new public key from a private key on disk

  ```ruby
  openssl_rsa_public_key '/etc/ssl_files/rsakey_des3.pub' do
    private_key_path '/etc/ssl_files/rsakey_des3.pem'
    private_key_pass 'something'
    action :create
  end
  ```

  Generate new public key by passing in a private key

  ```ruby
  openssl_rsa_public_key '/etc/ssl_files/rsakey_2.pub' do
    private_key_pass 'something'
    private_key_content "-----BEGIN RSA PRIVATE KEY-----
  Proc-Type: 4,ENCRYPTED
  DEK-Info: DES-EDE3-CBC,5EE0AE9A5FE3342E

  yb930kj5/4/nd738dPx6XdbDrMCvqkldaz0rHNw8xsWvwARrl/QSPwROG3WY7ROl
  EUttVlLaeVaqRPfQbmTUfzGI8kTMmDWKjw52gJUx2YJTYRgMHAB0dzYIRjeZAaeS
  ypXnEfouVav+jKTmmehr1WuVKbzRhQDBSalzeUwsPi2+fb3Bfuo1dRW6xt8yFuc4
  Akv1hCglymPzPHE2L0nSGjcgA2DZu+/S8/wZ4E63442NHPzO4VlLvpNvJrYpEWq9
  B5mJzcdXPeOTjqd13olNTlOZMaKxu9QShu50GreCTVsl8VRkK8NtwbWuPGBZlIFa
  jzlS/RaLuzNzfajaKMkcIYco9t7gN2DwnsACHKqEYT8248Ii3NQ+9/M5YcmpywQj
  WGr0UFCSAdCky1lRjwT+zGQKohr+dVR1GaLem+rSZH94df4YBxDYw4rjsKoEhvXB
  v2Vlx+G7Vl2NFiZzxUKh3MvQLr/NDElpG1pYWDiE0DIG13UqEG++cS870mcEyfFh
  SF2SXYHLWyAhDK0viRDChJyFMduC4E7a2P9DJhL3ZvM0KZ1SLMwROc1XuZ704GwO
  YUqtCX5OOIsTti1Z74jQm9uWFikhgWByhVtu6sYL1YTqtiPJDMFhA560zp/k/qLO
  FKiM4eUWV8AI8AVwT6A4o45N2Ru8S48NQyvh/ADFNrgJbVSeDoYE23+DYKpzbaW9
  00BD/EmUQqaQMc670vmI+CIdcdE7L1zqD6MZN7wtPaRIjx4FJBGsFoeDShr+LoTD
  rwbadwrbc2Rf4DWlvFwLJ4pvNvdtY3wtBu79UCOol0+t8DVVSPVASsh+tp8XncDE
  KRljj88WwBjX7/YlRWvQpe5y2UrsHI0pNy8TA1Xkf6GPr6aS2TvQD5gOrAVReSse
  /kktCzZQotjmY1odvo90Zi6A9NCzkI4ZLgAuhiKDPhxZg61IeLppnfFw0v3H4331
  V9SMYgr1Ftov0++x7q9hFPIHwZp6NHHOhdHNI80XkHqtY/hEvsh7MhFMYCgSY1pa
  K/gMcZ/5Wdg9LwOK6nYRmtPtg6fuqj+jB3Rue5/p9dt4kfom4etCSeJPdvP1Mx2I
  eNmyQ/7JN9N87FsfZsIj5OK9OB0fPdj0N0m1mlHM/mFt5UM5x39u13QkCt7skEF+
  yOptXcL629/xwm8eg4EXnKFk330WcYSw+sYmAQ9ZTsBxpCMkz0K4PBTPWWXx63XS
  c4J0r88kbCkMCNv41of8ceeGzFrC74dG7i3IUqZzMzRP8cFeps8auhweUHD2hULs
  XwwtII0YQ6/Fw4hgGQ5//0ASdvAicvH0l1jOQScHzXC2QWNg3GttueB/kmhMeGGm
  sHOJ1rXQ4oEckFvBHOvzjP3kuRHSWFYDx35RjWLAwLCG9odQUApHjLBgFNg9yOR0
  jW9a2SGxRvBAfdjTa9ZBBrbjlaF57hq7mXws90P88RpAL+xxCAZUElqeW2Rb2rQ6
  Cbz4/AtPekV1CYVodGkPutOsew2zjNqlNH+M8XzfonA60UAH20TEqAgLKwgfgr+a
  c+rXp1AupBxat4EHYJiwXBB9XcVwyp5Z+/dXsYmLXzoMOnp8OFyQ9H8R7y9Y0PEu
  -----END RSA PRIVATE KEY-----
  "
    action :create
  end
  ```
---
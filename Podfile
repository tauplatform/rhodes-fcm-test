platform :ios, '12.0'
use_frameworks!

pod 'Firebase/Auth'
pod 'Firebase/Firestore'
pod 'Firebase/Messaging'

# Specify stable gRPC versions
pod 'gRPC-Core', '~> 1.44.0'
pod 'gRPC-C++', '~> 1.44.0'

target 'rhorunner' do
end

post_install do |installer|
    installer.pods_project.targets.each do |target|
        if target.name == 'BoringSSL-GRPC'
          target.source_build_phase.files.each do |file|
            if file.settings && file.settings['COMPILER_FLAGS']
              flags = file.settings['COMPILER_FLAGS'].split
              flags.reject! { |flag| flag == '-GCC_WARN_INHIBIT_ALL_WARNINGS' }
              file.settings['COMPILER_FLAGS'] = flags.join(' ')
            end
          end
        end
        target.build_configurations.each do |config|
          if target.respond_to?(:product_type) and target.product_type == "com.apple.product-type.bundle"
            target.build_configurations.each do |config|
                config.build_settings['CODE_SIGNING_ALLOWED'] = 'NO'
            end
          end
        end
        if target.name == "Pods-rhorunner"
            puts "Updating #{target.name} OTHER_LDFLAGS"
            target.build_configurations.each do |config|

                xcconfig_path = config.base_configuration_reference.real_path

                # read from xcconfig to build_settings dictionary
                build_settings = Hash[*File.read(xcconfig_path).lines.map{|x| x.split(/\s*=\s*/, 2)}.flatten]

                # modify OTHER_LDFLAGS
                config_line = build_settings['OTHER_LDFLAGS']
                if (config_line != nil)
                    config_line = config_line.gsub("$(inherited) ","")
                    build_settings['OTHER_LDFLAGS'] = config_line
                    puts "updated OTHER_LDFLAGS = "+config_line
                end

                # write build_settings dictionary to xcconfig
                File.open(xcconfig_path, "w") do |file|
                  build_settings.each do |key,value|
                    file.write(key + " = " + value)
                  end
                end
            end
        end
    end
end

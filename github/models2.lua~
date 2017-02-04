require 'nngraph'

function defineGour_net(input_nc, output_nc, ngf)
   -- e0 = - nn.Tanh()

    e1 = - nn.SpatialConvolution(input_nc, ngf, 3, 3, 1, 1, 1, 1)
    --
    e2 = e1 -  nn.LeakyReLU(0.2, true) - nn.SpatialConvolution(ngf, ngf, 3, 3, 1, 1, 1, 1) - nn.SpatialBatchNormalization(ngf)
    --
    e3 = e2 -  nn.LeakyReLU(0.2, true) - nn.SpatialConvolution(ngf, ngf, 3, 3, 1, 1, 1, 1) - nn.SpatialBatchNormalization(ngf)
    --
    e4 = e3 -  nn.LeakyReLU(0.2, true) - nn.SpatialConvolution(ngf, ngf, 3, 3, 1, 1, 1, 1) - nn.SpatialBatchNormalization(ngf)
    --
    e5 = e4 -  nn.LeakyReLU(0.2, true) - nn.SpatialConvolution(ngf, ngf/2, 3, 3, 1, 1, 1, 1) - nn.SpatialBatchNormalization(ngf/2)
    --
    e6 = e5 -  nn.LeakyReLU(0.2, true) - nn.SpatialConvolution(ngf/2, 1, 3, 3, 1, 1, 1, 1) - nn.SpatialBatchNormalization(1)
    --
    d1_ = e6 -  nn.LeakyReLU(0.2, true) - nn.SpatialFullConvolution(1, ngf/2, 3, 3, 1, 1, 1, 1) - nn.SpatialBatchNormalization(ngf/2)
    --
    d2_= d1_ - nn.ReLU(true) - nn.SpatialFullConvolution(ngf/2, ngf, 3, 3, 1, 1, 1, 1) - nn.SpatialBatchNormalization(ngf)
    --
    d2 = {d2_,e4} - nn.CAddTable(true)
    --
    d3_ = d2 - nn.ReLU(true) - nn.SpatialFullConvolution(ngf, ngf, 3, 3, 1, 1, 1, 1) - nn.SpatialBatchNormalization(ngf)
    --
    d4_= d3_ - nn.ReLU(true) - nn.SpatialFullConvolution(ngf, ngf, 3, 3, 1, 1, 1, 1) - nn.SpatialBatchNormalization(ngf)
    --
    d4 = {d4_,e2} - nn.CAddTable(true)
    --
    d5_ = d4 - nn.ReLU(true) - nn.SpatialFullConvolution(ngf, ngf, 3, 3, 1, 1, 1, 1) - nn.SpatialBatchNormalization(ngf)
    --
    d61 = d5_ - nn.ReLU(true) - nn.SpatialFullConvolution(ngf, output_nc, 3, 3, 1, 1, 1, 1)
    d6 = d61 - nn.Identity()
    --
    o1 = d6 - nn.Tanh()
    
    netG = nn.gModule({e1},{o1})
      
    return netG
end

function defineD_basic(input_nc, output_nc, ndf)    
    n_layers = 3
    return defineD_n_layers(input_nc, output_nc, ndf, n_layers)
end


function defineD_n_layers(input_nc, output_nc, ndf, n_layers)
    
        local netD = nn.Sequential()
        
        netD:add(nn.SpatialConvolution(input_nc+output_nc, ndf, 4, 4, 2, 2, 1, 1))
        netD:add(nn.LeakyReLU(0.2, true))
        
        nf_mult = 1
        for n = 1, n_layers-1 do 
            nf_mult_prev = nf_mult
            nf_mult = math.min(2^n,8)
            netD:add(nn.SpatialConvolution(ndf * nf_mult_prev, ndf * nf_mult, 4, 4, 2, 2, 1, 1))
            netD:add(nn.SpatialBatchNormalization(ndf * nf_mult)):add(nn.LeakyReLU(0.2, true))
        end
        
        nf_mult_prev = nf_mult
        nf_mult = math.min(2^n_layers,8)
        netD:add(nn.SpatialConvolution(ndf * nf_mult_prev, ndf * nf_mult, 4, 4, 1, 1, 1, 1))
        netD:add(nn.SpatialBatchNormalization(ndf * nf_mult)):add(nn.LeakyReLU(0.2, true))
        netD:add(nn.SpatialConvolution(ndf * nf_mult, 1, 4, 4, 1, 1, 1, 1))       
        netD:add(nn.Sigmoid())
        
        return netD
    end
